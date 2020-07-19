<template>
  <div class="home">
    <!-- Temp Routing (DELETE BEFORE PROD PUSH) -->
    <router-link to="/posters">Posters</router-link>
    <br>
    <router-link to="/bleach">Leggings</router-link>
    <br>
    <router-link to="/book">Books</router-link>
    <br>
    <router-link to="/lettering">Lettering</router-link>
    <br>
    <router-link to="/chars">Characters</router-link>
    <br>
    <router-link to="/popup">Pop-up Book</router-link>

    <Loader v-if="showLoader"/>
    <CoolLightBox
      v-if="imagesToRender && !showLoader"
      :items="imageLinks"
      :index="imageIndex"
      loop
      @close="imageIndex = null">
    </CoolLightBox>
    <Portfolio v-if="imagesToRender && !showLoader" :images="imagesToRender" @setIndex="imageIndex = $event"/>
  </div>
</template>

<script>
import Portfolio from '@/components/Portfolio'
import Loader from '@/components/Loader'
import CoolLightBox from 'vue-cool-lightbox'
import 'vue-cool-lightbox/dist/vue-cool-lightbox.min.css'

export default {
  name: 'Home',
  props: {
  },
  components: {
    Portfolio,
    Loader,
    CoolLightBox
  },
  data () {
    return {
      contentfulClient: this.setupContentfulClient(),
      contentfulImages: {},
      currentPortfolioType: null,
      imagesToRender: null,
      imageIndex: null,
      contentTypes: ['posters', 'bleach', 'book', 'lettering', 'chars', 'popup'],
      showLoader: false
    }
  },
  mounted () {
    this.loadPath()
  },
  computed: {
    imageLinks () {
      const links = []
      if (this.imagesToRender) {
        for (let index = 0; index < this.imagesToRender.length; index++) {
          console.log(this.imagesToRender[index])
          const element = this.imagesToRender[index].fields.image.fields.file.url
          links.push(element)
        }
      }
      return links
    }
  },
  methods: {
    setupContentfulClient () {
      // Dane see our shared doc for keys
      const spaceId = 'paefqvuurocg'
      const accessToken = '863d0fa7ba79af2523059f2cee6b8276f63837d12b6d07b6889cfc8ccfbe883c'
      // contentful.js v4.x.x
      const contentful = require('contentful')
      return contentful.createClient({
        // This is the space ID. A space is like a project folder in Contentful terms
        space: spaceId,
        // This is the access token for this space. Normally you get both ID and the token in the Contentful web app
        accessToken: accessToken
      })
    },
    loadPath (to) {
      const toPath = to ? to.fullPath.replace(/\//, '') : this.$route.fullPath.replace(/\//, '')
      this.currentPortfolioType = toPath
      this.contentTypes.includes(toPath) ? this.getContentfulImages(toPath) : console.log('contentType does not exist')
    },
    getContentfulImages (contentType) {
      // check if contentType has already been loaded
      if (!this.contentfulImages[contentType]) {
        this.showLoader = true
        this.contentfulClient.getEntries({
          content_type: contentType
        })
          .then((response) => this.updateImages(response.items, contentType))
          .catch(console.error)
      } else {
        // already loaded this contentType, so set imagesToRender to currentPortfolioType
        this.imagesToRender = this.contentfulImages[this.currentPortfolioType]
      }
    },
    updateImages (responseItems, contentType) {
      // this.contentfulImages[contentType] = responseItems
      this.$set(this.contentfulImages, contentType, responseItems)
      this.showLoader = false
      console.log('this.contentfulImages', this.contentfulImages)
    }
  },
  watch: {
    contentfulImages: {

      // This will let Vue know to look inside the array
      deep: true,

      // We have to move our method to a handler field
      handler () {
        console.log('watcher', this.currentPortfolioType, this.contentfulImages)
        this.imagesToRender = this.contentfulImages[this.currentPortfolioType]
      }
    },
    $route (to, from) {
      // react to route changes...
      console.log('from: ', from.fullPath)
      console.log('to: ', to.fullPath)
      this.loadPath(to)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
</style>
