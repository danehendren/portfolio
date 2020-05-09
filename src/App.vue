<template>
  <div id="app">
    <SideNav :mobile="mobile"/>
    <Contact/>
    <router-view class="current-view"/>
  </div>
</template>

<script>
import SideNav from '@/components/SideNav'
import Contact from '@/components/Contact'
export default {
  name: 'App',
  components: {
    SideNav,
    Contact
  },
  mixins: [],
  data () {
    return {
      windowWidth: window.screen.width
    }
  },
  computed: {
    mobile () {
      return this.windowWidth < 768
    }
  },
  methods: {
    addWindowEventListener () {
      window.addEventListener('resize', (e) => {
        this.windowWidth = e.target.screen.width
      })
    }
  },
  mounted () {
    this.addWindowEventListener()
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
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}

.current-view {
  height: 100%;
  width: 100%;

  @media (min-width: 768px) {
    width: calc(100% - 320px);
    margin-left: 320px;
  }
}
</style>
