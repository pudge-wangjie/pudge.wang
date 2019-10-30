<template>
  <div class="button-grounp">
    <div class="g-left" @click="changeOutSearch">
      <span class="iconfont icon-fangdajing" v-if="!searchOutShow"></span>
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
      outListShow: false
    }
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
@import '../../../assets/css/header/search-s.less';
</style>