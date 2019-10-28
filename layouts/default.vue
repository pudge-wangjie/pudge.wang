<template>
  <el-container>
    <el-header>
      <Header />
    </el-header>
    <el-main>
      <nuxt />
    </el-main>
    <el-footer>Footer</el-footer>
    <bg-canvas/>
  </el-container>
</template>

<script>
import BgCanvas from '~/components/public/bgCanvas'
import Header from '~/components/public/header';

export default {
  components: {
    Header,
    BgCanvas
  }
}
</script>

<style lang="less">
@import "../assets/css/default/index.less";

</style>
