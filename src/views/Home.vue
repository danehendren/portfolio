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

    <div class="row no-gutters" v-if="contentfulImages">
      <!-- all assets src path -->
      <!-- <img class="portfolio-image m-2" v-for="image in contentfulImages" :key="image.id" :src="image.fields.file.url" alt=""> -->

      <!-- content type src path -->
      <img class="portfolio-image" v-for="image in contentfulImages" :key="image.id" :src="image.fields.image.fields.file.url" alt="">
      <Portfolio />
    </div>
  </div>
</template>

<script>
import Portfolio from '@/components/Portfolio'

export default {
  name: 'Home',
  props: {
    contentfulClient: Object
  },
  components: {
    Portfolio
  },
  data () {
    return {
      contentfulImages: null,
      portfolioType: 'home'
    }
  },
  mounted () {
  },
  methods: {
    getContentfulImages (contentType) {
      console.log('contentType', contentType)
      // For all assets use: client.getAssets()
      this.contentfulClient.getEntries({
        content_type: contentType
      })
        .then((response) => this.updateImages(response.items))
        .catch(console.error)

      // client.getAssets()
      //   .then((response) => this.updateImages(response.items))
      //   .catch(console.error)
    },
    updateImages (responseItems) {
      console.log(responseItems)
      this.contentfulImages = responseItems
    }
  },
  watch: {
    contentfulImages () {
      console.log('contentfulImages', this.contentfulImages)
    },
    $route (to, from) {
      // react to route changes...
      console.log('from: ', from.fullPath)
      console.log('to: ', to.fullPath)
      this.getContentfulImages(to.fullPath.replace(/\//, ''))
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.portfolio-image {
  height: 100%;
  width: 15%;
  border-radius: 2%;
  border: 4px solid lightblue;
}
</style>
