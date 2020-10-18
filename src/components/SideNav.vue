<template>
  <div>
    <div class="mobile-nav d-flex justify-content-between" v-if="mobileTabletDesktop === 'mobile'">
      <a href="/">Irina Schaefer</a>
      <a href="javascript:void(0);" class="icon" onclick="openMenu()" v-if="mobileTabletDesktop === 'mobile'" v-b-toggle.sidebar>
        <i class="fa fa-bars"></i>
      </a>
    </div>
    <b-sidebar :visible="showNav" :bg-variant="mobileTabletDesktop !== 'mobile' ? 'white' : light" :no-close-on-route-change="mobileTabletDesktop !== 'mobile'" :no-close-on-esc="mobileTabletDesktop !== 'mobile'" id="sidebar" :width="navWidth">
      <b-img alt="Logo Image" class="logo mt-2 skew p-0" fluid thumbnail :src="require('../assets/tester.jpg')"></b-img>
      <div class="px-3 py-2">
        <!-- <b-img src="https://picsum.photos/500/500/?image=54" fluid thumbnail></b-img> -->
        <div id="nav">
          <b-container>
            <b-row>
              <b-col cols="12" class="d-flex justify-content-start"><router-link to="/">portfolio</router-link></b-col>
              <b-col cols="12" class="d-flex justify-content-start"><router-link to="/about">about</router-link></b-col>
              <b-col cols="12" class="d-flex justify-content-start"><router-link to="/contact">contact</router-link></b-col>
            </b-row>
            <b-row class="mt-4">
              <b-col cols="4">Item</b-col>
              <b-col cols="4">Item</b-col>
              <b-col cols="4">Item</b-col>
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
    mobileTabletDesktop: {
      type: String,
      default: 'mobile'
    }
  },
  data () {
    return {
      showNav: this.mobileTabletDesktop !== 'mobile' // if initially NOT mobile show Nav
    }
  },
  computed: {
    navWidth () {
      return this.mobileTabletDesktop === 'mobile' ? '100%' : this.mobileTabletDesktop === 'tablet' ? '28%' : '320px'
    }
  },
  methods: {
    hideCloseIconOnDesktop () {
      document.querySelector('.b-sidebar-header .close').style.display = this.mobileTabletDesktop !== 'mobile' ? 'none' : 'inline-block'
    }
  },
  mounted () {
    this.$nextTick(function () { // Code that will run only after the entire view has been rendered
      this.hideCloseIconOnDesktop()
    })
  },
  watch: {
    mobileTabletDesktop () {
      this.hideCloseIconOnDesktop()
      this.showNav = this.mobileTabletDesktop !== 'mobile'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
#nav {
  padding-top: 30px;

  a {
    font-weight: 400;
    font-size: 1.75rem;
    color: #000000;
    text-decoration: none;

    &.router-link-exact-active {
      color: #E86E0E;
    }
  }
}

.logo {
  height: auto;
  width: 75%;

  @media (min-width: 768px) {
    width: calc(100% - 60px);
  }
}

.skew {
  transform: skewY(2deg);
  border: 4px solid black;
  box-shadow: -8px 4px 0px white, -10px 6px 0px black, -10px 2.5px 0px black, 12px 12px 0px black; //drastic
}

.mobile-nav {
  width: 100%;
  height: 45px;
  padding: 0 30px;
  font-size: 25px;

  a {
    color: black;
    height: 35px;
    margin-top: 5px;
  }
}
</style>
