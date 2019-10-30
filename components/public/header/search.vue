<template>
  <div class="search">
    <div class="search-inset">
      <div class="left">
        <input
          type="text"
          placeholder="全局标签搜索，如 css"
        />
      </div>
      <div class="right">
        <span class="iconfont icon-fangdajing"></span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {}
  }
}
</script>

<style lang="less" scoped>
@import '../../../assets/css/header/search.less';
</style>