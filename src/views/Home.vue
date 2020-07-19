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
      <b-row >
        <div class="container">
          <img src="../assets/categories/chars/digital-drawing-1.jpg" alt="Avatar" class="image">
          <div class="overlay">
            <div class="text">Text goes here</div>
          </div>
        </div>
        <div class="container">
          <img src="../assets/categories/chars/hand-drawn-cat-1.jpg" alt="Avatar" class="image">
          <div class="overlay">
            <div class="text">Text goes here</div>
          </div>
        </div>
        <div class="container">
          <img src="../assets/categories/chars/hand-drawn-dog-1.jpg" alt="Avatar" class="image">
          <div class="overlay">
            <div class="text">Text goes here</div>
          </div>
        </div>
        <div class="container">
          <img src="../assets/categories/posters/digital-poster-illufuchs-1.jpg" alt="Avatar" class="image">
          <div class="overlay">
            <div class="text">Text goes here</div>
          </div>
        </div>
          <!-- <b-img alt="#" class="tester"  fluid center :src="require('../assets/categories/print/print-lettering-illufuchs-1.png')"></b-img>
          <b-img alt="#" class="tester"  fluid center :src="require('../assets/categories/posters/digital-poster-illufuchs-2.jpg')"></b-img>
          <b-img alt="#" class="tester"  fluid center :src="require('../assets/categories/print/print-lettering-illufuchs-3.png')"></b-img>
          <b-img alt="#" class="tester"  fluid center :src="require('../assets/categories/print/print-lettering-illufuchs-4.png')"></b-img>
          <b-img alt="#" class="tester"  fluid center :src="require('../assets/categories/bleach/bleach-leggins-artist-1.jpg')"></b-img>
          <b-img alt="#" class="tester"  fluid center :src="require('../assets/categories/book/hand-painting-illufuchs-2.png')"></b-img>
          <b-img alt="#" class="tester"  fluid center :src="require('../assets/categories/chars/hand-drawn-dog-1.jpg')"></b-img>
          <b-img alt="#" class="tester"  fluid center :src="require('../assets/categories/chars/digital-drawing-1.jpg')"></b-img> -->
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
      index: null,
      counter: 0
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
.tester {
  object-fit: none;
  height: 250px;
  width: 250px;
  margin: 10px;
}
.container {
  position: relative;
  width: 50%;
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
  background-color: lightgrey;
}
.container:hover .overlay {
  opacity: 0.8;
}
.text {
  color: black;
  font-size: 20px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
}
</style>
