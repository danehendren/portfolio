<template>
  <div class="home">
    <div class="row" v-if="contentfulImages">
      <!-- all assets src path -->
      <img class="portfolio-image" v-for="image in contentfulImages" :key="image.id" :src="image.fields.file.url" alt="">

      <!-- portfolioImages content type src path -->
      <!-- <img class="portfolio-image" v-for="image in contentfulImages" :key="image.id" :src="image.fields.image.fields.file.url" alt=""> -->
    </div>
  </div>
</template>

<script>

export default {
  name: 'Home',
  props: {
    contentfulImages: {
      type: Array,
      default: null
    }
  },
  components: {
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
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.portfolio-image {
  height: 300px;
  width: 300px;
}
</style>
