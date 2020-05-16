<template>
  <div id="app">
    <SideNav :mobile="mobile"/>
    <Contact/>
    <router-view class="current-view" :contentfulImages="contentfulImages"/>
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
      windowWidth: window.screen.width,
      contentfulImages: null
    }
  },
  computed: {
    mobile () {
      return this.windowWidth < 768
    }
  },
  mounted () {
    this.addWindowEventListener()
    this.setupContentful()
  },
  methods: {
    addWindowEventListener () {
      window.addEventListener('resize', (e) => {
        this.windowWidth = e.target.screen.width
      })
    },
    setupContentful () {
      // Dane see our shared doc for keys
      const spaceId = ''
      const accessToken = ''

      // contentful.js v4.x.x
      const contentful = require('contentful')
      const client = contentful.createClient({
        // This is the space ID. A space is like a project folder in Contentful terms
        space: spaceId,
        // This is the access token for this space. Normally you get both ID and the token in the Contentful web app
        accessToken: accessToken
      })

      // For all assets use: client.getAssets()
      // client.getEntries({
      //   content_type: 'portfolioImages'
      // })
      client.getAssets()
        .then((response) => this.updateImages(response.items))
        .catch(console.error)
    },
    updateImages (responseItems) {
      console.log(responseItems)
      this.contentfulImages = responseItems
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
