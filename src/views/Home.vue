<template>
  <div class="home">
    <div v-if="contentfulImages">
      <b-container>
        <b-row class="justify-content-center">
          <!-- <b-img alt="#" class="tester" :src="require('../assets/illufuchs.png')"></b-img> -->
          <!-- <b-img class="tester" @click="setIndex(imageIndex)" v-for="(image,imageIndex) in contentfulImages" :key="image.id" :src="image.fields.file.url" alt=""></b-img> -->
        </b-row>
      </b-container>
      <CoolLightBox
        :items="imageLinks"
        :index="index"
        loop
        @close="index = null">
      </CoolLightBox>
    </div>
    <b-container>
      <b-row>
        <b-img alt="#" class="tester" :src="require('../assets/categories/drawings/moonlight.jpg')"></b-img>
        <b-img alt="#" class="tester" :src="require('../assets/categories/drawings/moonlight.jpg')"></b-img>
        <b-img alt="#" class="tester" :src="require('../assets/categories/drawings/moonlight.jpg')"></b-img>
        <b-img alt="#" class="tester" :src="require('../assets/categories/drawings/moonlight.jpg')"></b-img>
        <b-img alt="#" class="tester" :src="require('../assets/categories/drawings/moonlight.jpg')"></b-img>
        <b-img alt="#" class="tester" :src="require('../assets/categories/drawings/moonlight.jpg')"></b-img>
        <b-img alt="#" class="tester" :src="require('../assets/categories/drawings/moonlight.jpg')"></b-img>
        <b-img alt="#" class="tester" :src="require('../assets/categories/drawings/moonlight.jpg')"></b-img>
      </b-row>
    </b-container>
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
  // height: auto;
  // width: 250px;
  // object-fit: cover;
  // border-radius: 2%;
  // border: 2px solid lightcoral;
}
.tester {
  object-fit: none;
  height: 250px;
  width: 250px;
  margin: 10px;
}
</style>
