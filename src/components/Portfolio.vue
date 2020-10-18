<template>
  <div>
    <div class="col-12 d-flex justify-content-start my-3">
      <b-link v-if="!showMenu & !showLoader" size="sm" class="text-left text-dark d-block" to="/" variant="outline-dark">
        <b-icon icon="arrow-left-short" aria-hidden="true"></b-icon> Back to menu
      </b-link>
    </div>
    <div class="row portfolio-container">
      <div class="col-sm-3 portfolio-image-container" v-for="(image, imageIndex) in images" :key="image.id">
        <!-- content type src path -->
        <img class="portfolio-image" @click="$emit('setIndex', imageIndex)" :src="image.fields.image.fields.file.url" alt="">
        <div class="portfolio-title">{{ image.fields.title }}</div>
        <!-- <a href="#"><span class="fa fa-search-plus fa-5x"></span></a> -->
      </div>
    </div>
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
.portfolio-container {
  margin: 50px 0;
}

.portfolio-image-container {
  width: 100%;
  position: relative;
  transition: all 0.6s ease;
  transform: skewY(2deg);
  transform-origin: bottom;
  -webkit-backface-visibility: hidden;
  position: relative;
  display: inline-block; /* added */

  .portfolio-image {
    cursor: zoom-in;
    width: 100%;
    display: block;
    height: auto;
    margin-bottom: 60px;
    border: 4px solid black;
    padding: 0;
    transition: all 0.6s ease;

    &:hover {
      opacity: .8;
      box-shadow: -8px 4px 0px white, -10px 6px 0px black, -10px 2.5px 0px black, 12px 12px 0px black;
      border-right: 4px solid black;
      border-bottom: 4px solid black;
    }
  }

}

.portfolio-title {
  background-color: black;
  text-align: center;
  font-family: "HelveticaNeue-Light", "Helvetica Neue Light", "Helvetica Neue", Helvetica, Arial, "Lucida Grande", sans-serif;
  font-weight: 300;
  position: absolute;
  // bottom: 10%;
  width: 60%;
  color: white;
  right: 10%;
  top: -18px;
  font-size: 13px;
  // clip-path: polygon(50% 0, 0 100%, 100% 100%);
}
</style>
