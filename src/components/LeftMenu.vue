<template>
  <el-menu active-text-color="#ffd04b" background-color="#545c64" class="el-menu-vertical-demo" default-active="2"
    text-color="#fff" :collapse="!$store.state.HomeModule.navBool" @open="handleOpen" @close="handleClose" router>
    <template v-for="v in router.options.routes[1].children" :key="v.path">
      <el-sub-menu :index="v.path" v-if="v.children">
        <template #title>
          <el-icon>
            <component :is="v.meta.icon" />
          </el-icon>
          <span>{{ v.meta.title }}</span>
        </template>
        <el-menu-item-group :title="v.meta.title" v-for="val in v.children" :key="val.path">
          <el-menu-item :index="val.path">{{ val.meta.title }}</el-menu-item>
        </el-menu-item-group>
      </el-sub-menu>
      <el-menu-item :index="v.path" v-else>
        <el-icon>
          <component :is="v.meta.icon" />
        </el-icon>
        <span>{{ v.meta.title }}</span>
      </el-menu-item>
    </template>
  </el-menu>
</template>

<script lang="ts" setup>
import { onMounted } from "vue";
import { useRouter } from "vue-router";

import {
  TrendCharts, Memo, List
} from "@element-plus/icons-vue";
const handleOpen = (key: string, keyPath: string[]) => {
  console.log(key, keyPath);
};
const handleClose = (key: string, keyPath: string[]) => {
  console.log(key, keyPath);
};

let router = useRouter();
onMounted(() => {
  console.log("获取路由规则", router.options.routes[1].children);
});
</script>

<style scoped lang="scss">
.el-menu {
  border-right: none;
  background-color: rgb(50, 77, 69);

  .el-menu-item:focus,
  .el-menu-item:hover {
    background-color: rgb(41, 63, 56);
  }

  .el-sub-menu {
    ::v-deep(.el-sub-menu__title) {
      background-color: rgb(50, 77, 69) !important;
    }

    ::v-deep(.el-sub-menu__title):focus,
    ::v-deep(.el-sub-menu__title):hover {
      background-color: rgb(41, 63, 56) !important;
    }
    ::v-deep(.el-menu){
      background-color: rgb(50, 77, 69);
    }
  }
}
</style>