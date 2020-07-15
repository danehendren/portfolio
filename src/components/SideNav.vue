<template>
  <div>
    <div v-if="mobile" v-b-toggle.sidebar-1></div>
    <b-sidebar :visible="showNav" :no-close-on-route-change="!mobile" :no-close-on-esc="!mobile" id="sidebar-1" :width="navWidth">
      <!-- <b-img alt="Logo Image" class="logo mt-2" fluid rounded="circle" thumbnail :src="require('../assets/tester.jpg')"></b-img> -->
      <div class="px-3 py-2">
          <b-img alt="#" class="ph_logo" :src="require('../assets/illufuchs.png')"></b-img>
        <div id="nav">
          <b-container>
            <b-row>
              <b-col cols="12" class="d-flex justify-content-end"><router-link to="/">portfolio</router-link></b-col>
              <b-col cols="12" class="d-flex justify-content-end"><router-link to="/about">about</router-link></b-col>
              <b-col cols="12" class="d-flex justify-content-end"><router-link to="/contact">contact</router-link></b-col>
            </b-row>
            <b-row class="mt-4">
              <!-- <b-col cols="4"><a href="https://www.etsy.com/shop/DerIllufuchs" target="_blank"><b-img alt="Logo Image" class="logo" thumbnail :src="require('../assets/logos/etsyOne.png')"></b-img></a></b-col> -->
              <!-- <b-col cols="4"><a href="https://www.instagram.com/illufuchs/" target="_blank"><b-img alt="Logo Image" class="logo" thumbnail :src="require('../assets/logos/igOne.png')"></b-img></a></b-col> -->
              <!-- <b-col cols="4" v-on:click="emailMe"><b-img alt="Logo Image" class="logo" thumbnail :src="require('../assets/logos/mailOne.png')"></b-img></!-->
            </b-row>
          </b-container>
        </div>
      </div>
    </b-sidebar>
  </div>
</template>

<script>
export default {
  name: 'SideNav',
  props: {
    mobile: {
      type: Boolean,
      default: true
    }
  },
  data () {
    return {
      showNav: !this.mobile // if initially NOT mobile show Nav
    }
  },
  computed: {
    navWidth () {
      return this.mobile ? '100%' : '350px'
    }
  },
  methods: {
    hideCloseIconOnDesktop () {
      document.querySelector('.b-sidebar-header .close').style.display = !this.mobile ? 'none' : 'inline-block'
    },
    emailMe: function () {
      window.location.href = 'mailto:irinaschaefer.4@gmx.de'
    }
  },
  mounted () {
    this.$nextTick(function () { // Code that will run only after the entire view has been rendered
      this.hideCloseIconOnDesktop()
    })
  },
  watch: {
    mobile () {
      this.hideCloseIconOnDesktop()
      this.showNav = !this.mobile
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
// .ham{
//   height: 40px;
//   width: 40px;
//   float: right;
// }
.ph_logo {
  width: auto;
  height: 200px;
}
#nav {
  min-width: 250px;
  // background-color: lightblue
}
</style>
