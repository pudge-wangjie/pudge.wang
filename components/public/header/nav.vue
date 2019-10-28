<template>
  <nav>
    <li v-for="(item, index) in navList" 
      :key="index" 
      @click="jump(item.suffix)"
      :class="liClass(item, index)"
      >
      <div class="borderTop"></div>
      <div class="li-main">
        <span class="iconfont" :class="iconClass(item, index)"></span>
        <p class="title">{{ item.title }}</p>
      </div>
    </li>
  </nav>
</template>

<script>
export default {
  data() {
    return {
      navList: [
        {
          className: 'li1',
          iconName: 'icon-html5',
          title: 'HTML、CSS',
          suffix: 'css'
        },
        {
          className: 'li2',
          iconName: 'icon-js-square',
          title: 'JavaScript',
          suffix: 'js'
        },
        {
          className: 'li3',
          iconName: 'icon-vuejs',
          title: 'VUE',
          suffix: 'vue'
        },
        {
          className: 'li4',
          iconName: 'icon-react',
          title: 'React',
          suffix: 'react'
        },
        {
          className: 'li5',
          iconName: 'icon-node',
          title: 'node、其他',
          suffix: 'node'
        },
        {
          className: 'li6',
          iconName: 'icon-shiti-tianchong',
          title: '面试',
          suffix: 'interview'
        }
      ]
    }
  },
  computed: {
    currentUrl() {
      return this.$route.path;
    }
  },
  methods: {
    jump(target) {
      this.$router.push(target);
      // this.$store.commit('changeStage', target)
      // this.$store.commit('changeSelect', '')
      // sessionStorage.setItem('stage', target)
    },
    liClass(item, index) {
      return {
        [item.className]: true,
        hover: this.currentUrl.startsWith('/' + item.suffix)
      }
    },
    iconClass(item, index) {
      return {
        [item.iconName]: true,
        ['active' + (index + 1)]: true
      }
    }
  }
}
</script>

<style lang="less" scoped>
@import '../../../assets/css/header/nav.less';
</style>
