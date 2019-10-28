<template>
  <div class="search">
    <div class="search-inset" :class="{focusInBox: inputFocus}">
      <div class="left">
        <input
          type="text"
          placeholder="全局标签搜索，如 css"
          @focus="inputFocus = true"
          @blur="inputFocus = false"
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
    return {
      inputFocus: false
    }
  }
}
</script>

<style lang="less" scoped>
@import '../../../assets/css/header/search.less';
</style>