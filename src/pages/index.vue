<template >
  <div>
    <el-row :gutter="20">
      <!-- 骨架屏 -->
      <template v-if="panels.length == 0">
        <el-col :span="6" v-for="i in 4" :key="i">
          <el-skeleton style="width: 100%" animated loading>
            <template #template>
              <el-card shadow="hover" :body-style="{ padding: '20px' }">
                <template #header>
                  <div class="flex justify-between">
                    <el-skeleton-item variant="text" style="width: 50%" />
                    <el-skeleton-item variant="text" style="width: 10%" />
                  </div>
                </template>
                <el-skeleton-item variant="h3" style="width: 80%" />
                <el-divider />
                <div class="flex justify-between text-sm">
                  <el-skeleton-item variant="text" style="width: 30%" />
                  <el-skeleton-item variant="text" style="width: 30%" />
                </div>
              </el-card>
            </template>
          </el-skeleton>
        </el-col>
      </template>
      <!-- 数据屏 -->
      <el-col
        :span="6"
        :offset="0"
        v-for="(item, index) in panels"
        :key="index"
      >
        <el-card shadow="hover" :body-style="{ padding: '20px' }">
          <template #header>
            <div class="flex justify-between">
              <span>{{ item.title }}</span>
              <el-tag :type="item.unitColor" effect="plain">
                {{ item.unit }}
              </el-tag>
            </div>
          </template>
          <span class="text-3xl font-bold">
            <!-- {{ item.value }} -->
            <CountP :value="item.value"></CountP>
          </span>
          <el-divider />
          <div class="flex justify-between text-sm">
            <span>{{ item.subTitle }} </span>
            <span> {{ item.subValue }}</span>
          </div>
        </el-card>
      </el-col>
    </el-row>

    <el-row :gutter="20" class="mt-5">
      <el-col :span="12" :offset="0">
        <index-chart></index-chart>
      </el-col>

      <el-col :span="12" :offset="0">
        <index-card title="店铺" tip="店铺及其展示" :btns="goods"></index-card>
        <index-card title="交易" tip="交易及其展示" :btns="order"></index-card>
      </el-col>
    </el-row>
  </div>
</template>


<script setup>
import indexCard from '../components/indexCard.vue'
import indexChart from '../components/indexChart.vue'
import { getStatistics1, getStatistics2, } from '@/api/index.js'
import { ref } from 'vue'
import CountP from '@/components/CountP.vue'



const panels = ref([])
getStatistics1().then(res => {

  panels.value = res.panels
  // console.log(panels.value)
})

const goods = ref([])
const order = ref([])
getStatistics2().then(res => {
  goods.value = res.goods
  order.value = res.order
  // console.log(res)
})

</script>


<style lang="">
</style> 



