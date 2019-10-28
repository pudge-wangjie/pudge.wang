<template>
  <div class="search-button" @click="outSearchShow = !outSearchShow">
    <span class="iconfont icon-fangdajing" v-if="!outSearchShow"></span>
    <span class="iconfont icon-guanbi" v-else></span>
  </div>
</template>

<script>
export default {
  data() {
    return {
      outSearchShow: false
    }
  }
}
</script>

<style lang="less" scoped>
@import '../../../assets/css/header/search-m.less';
</style>