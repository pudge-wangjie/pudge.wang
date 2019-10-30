<template>
  <transition name="slide-fade">
    <div class="out-search" v-if="searchOutShow">
      <div class="inset-search">
        <div class="left">
          <input
            type="text"
            placeholder="e.g. float"
          >
        </div>
        <div class="right">
          <span class="iconfont icon-fangdajing"></span>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  data() {
    return {}
  },
  computed: {
    searchOutShow() {
      return this.$store.state.header.searchOutShow;
    }
  }
}
</script>

<style lang="less">
  @import '../../../assets/css/header/search-out.less';
</style>