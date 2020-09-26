<template>
  <v-form v-model="valid" class="px-5" ref="MyBrandForm">
    <v-text-field v-model="brand.name" label="输入品牌名称" required :rules="nameRules"/>
    <v-text-field v-model="brand.letter" label="输入品牌首字母" required :rules="letterRules"/>
    <v-cascader
      url="/item/category/list"
      multiple
      required
      v-model="brand.categories"
      label="请选择商品分类"
    />
    <!--layout布局组件  两列-->
    <v-layout row>
      <v-flex xs3>
        <span style="font-size: 16px;color:#444">品牌LOGO:</span>
      </v-flex>
      <v-flex>
        <v-upload
          v-model="brand.image"
          url="/upload/image"
          :multiple="false"
          :pic-width="250"
          :pic-height="90"
        />
      </v-flex>
    </v-layout>
    <v-layout class="my-4" row>
      <v-spacer/>
      <v-btn @click="submit" color="primary">提交</v-btn>
      <v-btn @click="clear">重置</v-btn>
    </v-layout>
  </v-form>
</template>

<script>
  export default {
    name: "MyBrandForm",
    props:{
      oldBrand:{
        type:Object
      },
      isEdit:{
        type: Boolean,
        default:false
      }
    },
    data() {
      return {
        valid: false,//表单验证结果标记
        brand: {
          name: '',//品牌名称
          letter: '',//品牌首字母
          image: '',//品牌logo
          categories: []//品牌所属分类
        },
        nameRules: [
          v => !!v || "品牌名称不能为空",
          v => v.length > 1 || "品牌名称至少2位"
        ],
        letterRules: [
          v => !!v || "首字母不能为空",
          v => /^[a-zA-Z]{1}$/.test(v) || "品牌字母只能是1个字母"
        ]
      }
    },
    methods: {
      submit() {
          //提交表单
        console.log(this);

        if (this.$refs.MyBrandForm.validate()){
          // 2、定义一个请求参数对象，通过解构表达式来获取brand中的属性
          const {categories,letter,...params} = this.brand;
          // 3、数据库中只要保存分类的id即可，因此我们对categories的值进行处理,只保留id，并转为字符串
          params.cids = categories.map(c => c.id).join(",");
          // 4、将字母都处理为大写
          params.letter = letter.toUpperCase();
          // 5、将数据提交到后台
          //this.$http.post('/item/brand',this.$qs.stringify(params))
          this.$http({
            method: this.isEdit ? 'put':'post',//动态判断是put还是post
            url: '/item/brand',
            data: this.$qs.stringify(params)
          }).then(() =>{
              this.$emit("close")
              this.$message.success("保存成功");
            }).catch(() => {
              this.$message.error("保存失败")
          })
        }
      },
      clear() {
         this.$refs.MyBrandForm.reset();
         this.categories = [];
      },
    },
    watch:{
      oldBrand:{
        handler(val){
          if (val){
            this.brand = Object.deepCopy(val)
          } else {
            this.brand={
              name:'',
              letter:'',
              image:'',
              categories:[],
            }
          }
        },

        deep:true
      }
    }
  }
</script>

<style scoped>

</style>
