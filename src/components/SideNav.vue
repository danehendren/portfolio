<template>
  <div>
    <b-button v-if="mobile" v-b-toggle.sidebar-1>Toggle Sidebar</b-button>
    <b-sidebar :visible="showNav" :no-close-on-route-change="!mobile" :no-close-on-esc="!mobile" id="sidebar-1" title="Ira Stuff" :width="navWidth">
      <div class="px-3 py-2">
        <!-- <b-img src="https://picsum.photos/500/500/?image=54" fluid thumbnail></b-img> -->
        <div id="nav">
          <b-container class="bv-example-row">
            <b-row class="justify-content-md-center">
              <b-col cols="12" class="mb-2"><router-link to="/">Portfolio</router-link></b-col>
              <b-col cols="12" class="mb-2"><router-link to="/about">About</router-link></b-col>
              <b-col cols="12" class="mb-2"><router-link to="/contact">Contact</router-link></b-col>
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
      return this.mobile ? '100%' : '320px'
    }
  },
  methods: {
    hideCloseIconOnDesktop () {
      document.querySelector('.b-sidebar-header .close').style.display = !this.mobile ? 'none' : 'inline-block'
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
</style>
