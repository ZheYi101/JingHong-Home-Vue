<script setup lang="ts">
import { onBeforeMount, onMounted, ref, toRef } from "vue";
import { RouterView } from "vue-router";
import { usePageStore } from "./stores/pages";
import { welcome } from "./utils/const";
const pageStore = usePageStore();
var pageSize = ref(1440);
function handleResize() {
  let width = document.documentElement.clientWidth;
  if (width >= 1024) {
    pageStore.pageType = "normal";
    document.querySelector("body")?.setAttribute("style", "min-width: 1440px");
  } else if (width >= 768) {
    pageStore.pageType = "middle";
    document.querySelector("body")?.setAttribute("style", "min-width: 420px");
  } else {
    pageStore.pageType = "mini";
    document.querySelector("body")?.setAttribute("style", "min-width: 320px");
  }
}
onMounted(() => {
  handleResize();
  window.onresize = () => {
    handleResize();
  };
  //字符画欢迎花活
  welcome()
});
</script>

<template>
  <router-view name="navbar" />
  <router-view />
</template>

<style>
.root {
  --body-min-width: v-bind("pageSize");
}

@font-face {
  font-family: "SC-VF";
  src: url("https://download.tooc.xlj0.com/uploads/22/jhhome/public/font/SourceHanSansSC-VF.otf");
}

#app {
  width: 100%;
  font-family: "SC-VF";
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
