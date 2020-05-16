<template>
  <div class="home">
    <div class="row p-4" v-if="contentfulImages">
      <!-- all assets src path -->
      <!-- <img class="portfolio-image m-2" v-for="image in contentfulImages" :key="image.id" :src="image.fields.file.url" alt=""> -->
      <!-- portfolioImages content type src path -->
        <b-img class="portfolio-image m-3" fluid rounded v-for="image in contentfulImages" :key="image.id" :src="image.fields.file.url" alt=""></b-img>
      <!-- <b-img alt="Profile Image" class="profile mt-5" fluid rounded="circle" thumbnail :src="require('../assets/tester.jpg')"></b-img> -->

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
  height: 100%;
  width: 15%;
  // object-fit: cover;
  // border-radius: 2%;
  border: 2px solid lightcoral;
}
</style>
