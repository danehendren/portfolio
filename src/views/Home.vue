<template>
  <div class="home">
    <router-link to="/illustrations">Illustrations</router-link>
    <br>
    <router-link to="/graphic-design">Graphic Design</router-link>
    <br>
    <router-link to="/leggings">Leggings</router-link>

    <div class="row no-gutters" v-if="contentfulImages">
      <!-- all assets src path -->
      <img class="portfolio-image m-2" v-for="image in contentfulImages" :key="image.id" :src="image.fields.file.url" alt="">

      <!-- portfolioImages content type src path -->
      <!-- <img class="portfolio-image" v-for="image in contentfulImages" :key="image.id" :src="image.fields.image.fields.file.url" alt=""> -->
    </div>
    <Portfolio />
  </div>
</template>

<script>
import Portfolio from '@/components/Portfolio'

export default {
  name: 'Home',
  props: {
    contentfulImages: {
      type: Array,
      default: null
    }
  },
  components: {
    Portfolio
  },
  data () {
    return {
      images: null
    }
  },
  mounted () {
    console.log('contentfulImages', this.contentfulImages)
  },
  methods: {
  },
  watch: {
    contentfulImages () {
      console.log('contentfulImages', this.contentfulImages)
    },
    $route (to, from) {
      // react to route changes...
      console.log('from: ', from.fullPath)
      console.log('to: ', to.fullPath)
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
