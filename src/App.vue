<template>
  <div id="app">
    <SideNav :mobile="mobile"/>
    <Contact/>
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
  font-family: PT Sans Narrow, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 70px;

  a {
    font-weight: 400;
    font-size: 1.75rem;
    color: #000000;
    text-decoration: none;

    &.router-link-exact-active {
      color: #E86E0E;
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
