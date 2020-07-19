<template>
  <div>
    <!-- all assets src path -->
    <!-- <img class="portfolio-image m-2" v-for="image in contentfulImages" :key="image.id" :src="image.fields.file.url" alt=""> -->

    <!-- content type src path -->
    <img class="portfolio-image" v-for="image in images" :key="image.id" :src="image.fields.image.fields.file.url" alt="">
  </div>
</template>

<script>
export default {
  name: 'Portfolio',
  props: {
    mobileTabletDesktop: {
      type: String,
      default: 'mobile'
    },
    images: {
      type: Array,
      default: null
    }
  },
  data () {
    return {
    }
  },
  computed: {
  },
  methods: {
  },
  mounted () {
  },
  watch: {
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
