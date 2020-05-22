<template>
  <div class="home">
    <div class="row p-4" v-if="contentfulImages">
      <!-- all assets src path -->
      <!-- <img class="portfolio-image m-2" v-for="image in contentfulImages" :key="image.id" :src="image.fields.file.url" alt=""> -->
      <!-- portfolioImages content type src path -->
        <b-img class="portfolio-image m-3" @click="setIndex(imageIndex)" fluid rounded v-for="(image,imageIndex) in contentfulImages" :key="image.id" :src="image.fields.file.url" alt=""></b-img>
        <!-- <b-col sm="12" lg="6"><b-img class="portfolio-image m-3" @click="setIndex(imageIndex)" fluid rounded v-for="(image,imageIndex) in contentfulImages" :key="image.id" :src="image.fields.file.url" alt=""></b-img></b-col> -->

      <CoolLightBox
        :items="imageLinks"
        :index="index"
        loop
        @close="index = null">
      </CoolLightBox>
      <!-- <b-img alt="Profile Image" class="profile mt-5" fluid rounded="circle" thumbnail :src="require('../assets/tester.jpg')"></b-img> -->
    </div>
  </div>
</template>

<script>
import CoolLightBox from 'vue-cool-lightbox'
import 'vue-cool-lightbox/dist/vue-cool-lightbox.min.css'
export default {
  name: 'Home',
  props: {
    contentfulImages: {
      type: Array,
      default: null
    }
  },
  components: {
    CoolLightBox
  },
  data () {
    return {
      images: null,
      index: null
    }
  },
  computed: {
    imageLinks () {
      const links = []
      for (let index = 0; index < this.contentfulImages.length; index++) {
        const element = this.contentfulImages[index].fields.file.url
        console.log('mine', element)
        links.push(element)
      }
      console.log('my links', links)
      return links
    }
  },
  mounted () {
    console.log('contentfulImages', this.contentfulImages)
  },
  methods: {
    setIndex (index) {
      this.index = index
    }
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
  width: 25%;
  // object-fit: cover;
  // border-radius: 2%;
  // border: 2px solid lightcoral;
}
</style>
