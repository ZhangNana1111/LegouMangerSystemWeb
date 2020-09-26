<template>
  <v-container fluid grid-list-md>
    <v-layout>
      <v-flex lg3>
        <v-card>
          <v-card-text class="px2" align="center">
            <div class="out-border">
              <div class="layout-title"><h3>乐购后台管理项目Git地址</h3></div>
              <div class="color-main address-content">
                <a href="https://github.com/macrozheng/mall">LeGou_Manger</a>
              </div>
            </div>
          </v-card-text>
        </v-card>
      </v-flex>
      <v-flex lg3>
        <v-card>
          <v-card-text class="px2" align="center">
            <div class="out-border">
              <div class="layout-title"><h3>乐购后台管理项目Git地址</h3></div>
              <div class="color-main address-content">
                <a href="https://github.com/macrozheng/mall">LeGou_Manger</a>
              </div>
            </div>
          </v-card-text>
        </v-card>
      </v-flex>
      <v-flex lg3>
        <v-card>
          <v-card-text class="px2" align="center">
            <div class="out-border">
              <div class="layout-title"><h3>乐购后台管理项目Git地址</h3></div>
              <div class="color-main address-content">
                <a href="https://github.com/macrozheng/mall">LeGou_Manger</a>
              </div>
            </div>
          </v-card-text>
        </v-card>
      </v-flex>
      <v-flex lg3>
        <v-card height="230px" width="250px">
          <v-card-text class="px2" align="center" >
            <div style="text-align: center">
              <img width="100px" height="100px" src="../assets/images/gongzongghao.jpeg">
            </div>
            <div style="text-align: center">乐购项目全套学习教程连载中！</div>
            <div style="text-align: center;margin-top: 5px"><span class="color-main">关注公号</span>，第一时间获取。</div>
          </v-card-text>
        </v-card>
      </v-flex>
    </v-layout>

    <v-layout row wrap>
      <v-flex xs10 md6>
        <v-card>
          <v-card-text class="px2">
            <div ref="sale" style="width: 100%;height:350px"></div>
          </v-card-text>
        </v-card>
      </v-flex>
      <v-flex xs10 md6>
        <v-card >
          <v-card-text class="px2">
            <div ref="pie" style="width: 100%;height:350px"></div>
          </v-card-text>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>



</template>

<script>
  // 引入 ECharts 主模块
  var echarts = require('echarts/lib/echarts');
  require('echarts/lib/chart/bar');
  require('echarts/lib/chart/pie');

  export default {
    name: "dashboard",
    data(){
      return {

      }
    },
    mounted(){
      this.$nextTick(() => {
        var sale = echarts.init(this.$refs.sale);

        // 指定图表的配置项和数据
        var option = {
          title: {
            text: '销售统计'
          },
          tooltip: {},
          legend: {
            data:['销量']
          },
          xAxis: {
            data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
          },
          yAxis: {},
          series: [{
            name: '销量',
            type: 'bar',
            data: [5, 20, 36, 10, 10, 20]
          }]
        };

        // 使用刚指定的配置项和数据显示图表。
        sale.setOption(option);

        const pie = echarts.init(this.$refs.pie);

        pie.setOption({
          roseType: 'angle',
          title: {
            text: '访问来源'
          },
          series : [
            {
              name: '访问来源',
              type: 'pie',
              radius: '55%',
              data:[
                {value:235, name:'视频广告'},
                {value:274, name:'联盟广告'},
                {value:310, name:'邮件营销'},
                {value:335, name:'直接访问'},
                {value:400, name:'搜索引擎'}
              ]
            }
          ],
          itemStyle: {
            emphasis: {
              // 阴影的大小
              shadowBlur: 200,
              // 阴影水平方向上的偏移
              shadowOffsetX: 0,
              // 阴影垂直方向上的偏移
              shadowOffsetY: 0,
              // 阴影颜色
              shadowColor: 'rgba(0, 0, 0, 0.5)'
            }
          }
        })
      })
    }
  }
</script>

<style scoped>

  .layout-title {
    color: #606266;
    padding: 15px 20px;
    background: #F2F6FC;
    font-weight: bold;
    width: 230px;
  }


  .out-border {
    width: 200px;
    height: 200px;
    align-content: center;
  }

  .address-content{
    padding: 20px;
    font-size: 18px
  }
</style>
