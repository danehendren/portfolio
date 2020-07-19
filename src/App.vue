<template>
  <div id="app">
    <SideNav :mobileTabletDesktop="mobileTabletDesktop"/>
    <router-view class="current-view"/>
  </div>
</template>

<script>
import SideNav from '@/components/SideNav'
export default {
  name: 'App',
  components: {
    SideNav
  },
  mixins: [],
  data () {
    return {
      windowWidth: window.screen.width
    }
  },
  computed: {
    mobileTabletDesktop () {
      return this.windowWidth < 768 ? 'mobile' : this.windowWidth < 1024 ? 'tablet' : 'desktop'
    }
  },
  mounted () {
    this.addWindowEventListener()
  },
  methods: {
    addWindowEventListener () {
      window.addEventListener('resize', (e) => {
        this.windowWidth = e.target.screen.width
      })
    }
  },
  watch: {}
}
</script>

<style lang="scss">
body {
  width: 100%;
  height: 100vh;
}

#app {
  height: 100%;
  width: 100%;
  font-family: PT Sans Narrow, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.current-view {
  height: 100%;
  width: 100%;
  overflow: scroll;

  @media (min-width: 768px) {
    width: calc(100% - 28%) !important;
    margin-left: 28% !important;
    padding: 0px 35px 0 25px !important;
  }

  @media (min-width: 1024px) {
    width: calc(100% - 320px) !important;
    margin-left: 320px !important;
    padding: 0px 35px 0 25px !important;
  }
}
</style>
