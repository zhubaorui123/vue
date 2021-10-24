<template>
  <div class="dashboard-editor-container">
    <!-- 第一个组件 -->
    <PanelGroup @handleSetLineChartData="handleSetLineChartData"/>

    <div class="chart-line">
      <!-- 第二个组件：折线图-->
      <line-chart :chart-data="lineChartData" :yTittle="yTitle"/>
    </div>

    <el-row :gutter="20" class="chart-row">
      <el-col :xs="24" :sm="24" :lg="12">
        <el-card>
          <!-- 第三个组件:柱状图组件 -->
          <bar-chart />
        </el-card>
      </el-col>
      <el-col :xs="24" :sm="24" :lg="12">
        <el-card>
          <!-- 第四个组件:饼状图 -->
          <pie-chart />
        </el-card>
      </el-col>
    </el-row>

    <el-row :gutter="20">
      <el-col :xs="24" :sm="24" :lg="8">
        <el-card>
          <!-- 第五个组件:折线图 -->
          <line-chart2 />
        </el-card>
      </el-col>
      <el-col :xs="24" :sm="24" :lg="8">
        <el-card>
          <!-- 第六个组件:柱状图 -->
          <bar-chart2 />
        </el-card>
      </el-col>
      <el-col :xs="24" :sm="24" :lg="8">
        <el-card>
          <!-- 第七个组件：饼状图 -->
          <pie-chart2/>
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>

<script>
//引入相应的子组件-----图标组件（七个）
//echarts开发
import PanelGroup from './components/PanelGroup'
import LineChart from './components/LineChart'
import BarChart from './components/BarChart'
import PieChart from './components/PieChart'
//v-chart
import LineChart2 from './components/LineChart2'
import BarChart2 from './components/BarChart2'
import PieChart2 from './components/PieChart2'

//准备模拟服务器的数据
const lineChartDatas = {
  purchases: {
    expectedData: [80, 100, 121, 104, 105, 90, 100],
    actualData: [120, 90, 100, 138, 142, 130, 130]
  },
  shoppings: {
    expectedData: [130, 140, 141, 142, 145, 150, 160],
    actualData: [120, 82, 91, 154, 162, 140, 130]
  },
  newUsers: {
    expectedData: [100, 120, 161, 134, 105, 160, 165],
    actualData: [120, 82, 91, 154, 162, 140, 145]
  },
  messages: {
    expectedData: [200, 192, 120, 144, 160, 130, 140],
    actualData: [180, 160, 151, 106, 145, 150, 130]
  },
}

//准备的数据：给子组件传递的-----图表的标题
const yTitles = {
  purchases: '交易金额(万元)',
  shoppings: '订单数量(个)',
  newUsers: '客户数量(人)',
  messages: '消息数量(条)',
}

export default {
  name: 'DashBoard',

  data() {
    return {
      lineChartDatas: [],
      //父组件给子组件传递的图表的数据
      lineChartData: {},
      //父组件给子组件传递的数据【图表的标题】
      yTitle: yTitles.purchases
    }
  },
  
  mounted () {
    //这里通过定时器（1S执行），在模拟服务器返回的数据
    setTimeout(() => {
      this.lineChartDatas = lineChartDatas
      this.lineChartData = lineChartDatas.purchases
    }, 1000);
  },

  methods: {
    handleSetLineChartData(type) {
      this.yTitle = yTitles[type]
      this.lineChartData = lineChartDatas[type]
    }
  },
  //注册子组件
  components: {
    PanelGroup,
    LineChart,
    BarChart,
    PieChart,
    LineChart2,
    BarChart2,
    PieChart2,
  }
}
</script>

<style lang="scss" scoped>
.dashboard-editor-container {
  padding: 32px;
  background-color: rgb(240, 242, 245);
  .chart-line {
    background:#fff;
    padding:16px 0 0 16px;
    margin-bottom:32px;
  }
  .chart-row {
    margin-bottom: 32px;
  }
}
</style>
