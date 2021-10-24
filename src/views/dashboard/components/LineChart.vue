<template>
  <!--容器-->
  <div :style="{ width, height }" ref="cur"></div>
</template>

<script>
//引入echarts核心库
import echarts from "echarts";
export default {
  name: "",
  data(){
    return{
      //组件实例的自身属性，用于接受echarts实例
      myChart:null,
    }
  }
  ,
  props: {
    //由父组件决定子组件的w|h
    width: {
      type: String,
      default: "100%",
    },
    height: {
      type: String,
      default: "350px",
    },
    yTittle: {
      type: String,
      default: "",
    },
    //异步数据
    chartData: {
      type: Object,
      default: {},
    },
  },
  //组件挂载完毕
  mounted() {
    // 基于准备好的dom，初始化echarts实例
    this.myChart = echarts.init(this.$refs.cur);
    this.initData();
  },
  methods: {
    initData(actualData=[],expectedData=[]) {
      // 指定图表的配置项和数据
      var option = {
        //标题
        title: {
          //标题的设置项
          text: this.yTittle,
          //显示与隐藏标题
          show: true,
          //设置标题的颜色
          textStyle: {
            //颜色设置
            color: "black",
          },
        },
        //提示框组件
        tooltip: {
          //坐标轴指示器配置项
          axisPointer: {
            type: "cross",
          },
        },
        //图例组件
        legend: {
          data: ["销量", "军事"],
        },
        //x轴的配置项
        xAxis: {
          data: ["衬衫", "羊毛衫", "雪纺衫", "裤子", "高跟鞋", "袜子"],
          show: true,
          //留白的设置
          boundaryGap: false,
        },
        //y轴的配置项
        yAxis: {},
        //系列的设置
        series: [
          {
            name: "销量",
            type: "line",
            //设置线与提示组件的颜色
            itemStyle: {
              color: "red",
            },
            data: actualData,
            //设置填充的颜色
            areaStyle: {
              color: "pink",
            },
          },
          {
            name: "军事",
            type: "line",
            data: expectedData,
            //设置线的颜色
            lineStyle: {
              color: "purple",
            },
          },
        ],
      };
      // 使用刚指定的配置项和数据显示图表。
      this.myChart.setOption(option);
    },
  },
  //监听
  watch:{
    chartData(newValue){
       //再次调用初始化数据的方法-给echarts图标赋予服务器返回的数据进行展示
       this.initData(newValue.actualData,newValue.expectedData);
    }
  }
};
</script>

<style scoped>
</style>
