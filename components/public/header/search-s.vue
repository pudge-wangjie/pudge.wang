<template>
  <div class="button-grounp">
    <div class="g-left" @click="outSearchShow = !outSearchShow">
      <span class="iconfont icon-fangdajing" v-if="!outSearchShow"></span>
      <span class="iconfont icon-guanbi" v-else></span>
    </div>
    <div class="g-right" :class="{rightActive: outListShow}" @click="outListShow = !outListShow">
      <span class="iconfont icon-liebiao" v-if="!outListShow"></span>
      <span class="iconfont icon-guanbi" v-else></span>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      outSearchShow: false,
      outListShow: false
    }
  }
}
</script>

<style lang="less" scoped>
@import '../../../assets/css/header/search-s.less';
</style>