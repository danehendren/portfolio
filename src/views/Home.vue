<template>
  <div class="home">
    <!-- Temp Routing (DELETE BEFORE PROD PUSH) -->
    <div v-if="!showMenu" class="row no-gutters">
      <div class="col-6 col-lg-3">
        <router-link to="/posters">
          <div class="img-container">
            <img src="@/assets/menu/menu1.jpg" alt="Avatar" class="image">
            <div class="overlay">
              <div class="text">Posters</div>
            </div>
          </div>
        </router-link>
      </div>
    <div class="col-6 col-lg-3">
      <router-link to="/bleach">
        <div class="img-container">
            <img src="@/assets/menu/menu2.jpg" alt="Avatar" class="image">
            <div class="overlay">
              <div class="text">Leggings</div>
            </div>
        </div>
      </router-link>
    </div>
    <div class="col-6 col-lg-3">
      <router-link to="/book">
        <div class="img-container">
            <img src="@/assets/menu/menu3.jpg" alt="Avatar" class="image">
            <div class="overlay">
              <div class="text">Books</div>
            </div>
        </div>
      </router-link>
    </div>
    <div class="col-6 col-lg-3">
      <router-link to="/lettering">
        <div class="img-container">
            <img src="@/assets/menu/menu1.jpg" alt="Avatar" class="image">
            <div class="overlay">
              <div class="text">lettering</div>
            </div>
          </div>
      </router-link>
    </div>
    <div class="col-6 col-lg-3">
      <router-link to="/chars">
        <div class="img-container">
            <img src="@/assets/menu/menu1.jpg" alt="Avatar" class="image">
            <div class="overlay">
              <div class="text">Characters</div>
            </div>
          </div>
      </router-link>
    </div>
    <div class="col-6 col-lg-3">
      <router-link to="/popup">
        <div class="img-container">
            <img src="@/assets/menu/menu2.jpg" alt="Avatar" class="image">
            <div class="overlay">
              <div class="text">Pop Up Book</div>
            </div>
          </div>
      </router-link>
    </div>
    <div class="col-6 col-lg-3">
      <router-link to="/illustrator">
        <div class="img-container">
            <img src="@/assets/menu/menu3.jpg" alt="Avatar" class="image">
            <div class="overlay">
              <div class="text">Illustrator</div>
            </div>
          </div>
      </router-link>
    </div>
    <div class="col-6 col-lg-3">
      <router-link to="/photoshop">
        <div class="img-container">
            <img src="@/assets/menu/menu1.jpg" alt="Avatar" class="image">
            <div class="overlay">
              <div class="text">photoshop</div>
            </div>
          </div>
      </router-link>
    </div>
  </div>
    <Loader v-if="showLoader"/>
  <div>
        <router-link to="/">
          <button>Back Please</button>
        </router-link>
    </div>
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
      showLoader: false,
      showMenu: this.$route.fullPath.length > 1
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
      const spaceId = ''
      const accessToken = ''
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
      this.showMenu = to.fullPath.length > 1
      this.loadPath(to)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.img-container {
  position: relative;
  width: 100%;
}

.image {
  display: block;
  width: 100%;
  height: auto;
}

.overlay {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  height: 100%;
  width: 100%;
  opacity: 0;
  transition: .5s ease;
  background-color: lightblue;
}

.img-container:hover .overlay {
  opacity: 0.8;
}

.text {
  color: black;
  font-size: 20px;
  position: absolute;
  top: 50%;
  left: 50%;
  -webkit-transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%);
  text-align: center;
}
</style>
