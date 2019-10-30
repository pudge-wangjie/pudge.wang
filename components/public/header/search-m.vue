<template>
  <div class="search-button" @click="changeOutSearch">
    <span class="iconfont icon-fangdajing" v-if="!searchOutShow"></span>
    <span class="iconfont icon-guanbi" v-else></span>
  </div>
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
  },
  methods: {
    changeOutSearch() {
      if (this.searchOutShow) {
        this.$store.commit('header/change', false)
      } else {
        this.$store.commit('header/change', true)
      }
    }
  }
}
</script>

<style lang="less" scoped>
@import '../../../assets/css/header/search-m.less';
</style>