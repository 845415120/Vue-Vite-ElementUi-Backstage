<template>
  <div class="common-layout">
    <el-container>
      <el-header class="flex">
        <f-header></f-header>
      </el-header>
      <el-container>
        <el-aside :width="$store.state.asideWidth">
          <f-menu></f-menu>
        </el-aside>
        <el-main>
          <router-view> </router-view>
          <!-- <f-tag-list></f-tag-list> -->
          <!-- 内容部分 -->
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>
<script setup>
import FHeader from "./components/FHeader.vue"
import FMenu from "./components/FMenu.vue"
import FTagList from "./components/FTagList.vue";

</script>
<style>
main.el-main {
  width: 1100px;
}
</style>