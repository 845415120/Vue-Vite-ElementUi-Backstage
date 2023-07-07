<template>
  <el-card shadow="never" :body-style="{ padding: '20px' }">
    <template #header>
      <div class="flex justify-between">
        <span class="text-sm">订单统计</span>
        <div>
          <el-check-tag
            v-for="(item, index) in options"
            :key="index"
            :checked="current == item.value"
            style="margin-right: 8px"
            >{{ item.text }}</el-check-tag
          >
        </div>
      </div>
    </template>
    <div id="chart" style="width: 300px; height: 300px"></div>
  </el-card>
</template>

<script setup>
import * as echarts from 'echarts'
import { ref, onMounted } from 'vue'
import { getStatistics3 } from '@/api/index.js'
const current = ref("week")
const options = [
  {
    text: '近一周',
    value: 'week'
  }

]

var myChart = null

onMounted(() => {
  var chartDom = document.getElementById('chart')
  myChart = echarts.init(chartDom)
  getData()
})

function getData () {
  let option = {
    xAxis: {
      type: 'category',
      data: []
    },
    yAxis: {
      type: 'value'
    },

    series: [
      {
        data: [],
        type: 'bar',
        showBackground: true,
        backgroundStyle: {
          color: 'rgba(180, 180, 180, 0.2)'
        }

      }
    ]
  }
  getStatistics3(current.value).then(res => {
    option.xAxis.data = res.x
    option.series[0].data = res.y
    myChart.setOption(option)
  })
}


</script>