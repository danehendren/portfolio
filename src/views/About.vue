<template>
  <b-container>
    <b-row class="vh-100 text-center" align-v="center" align-h="center">
        <b-col cols="5">
          <b-img alt="#" :src="require('../assets/ph_photo.jpg')"></b-img>
        </b-col>
    </b-row>
    <b-row class="vh-100 text-center" align-h="center">
      <b-col>
        <p>they just had some text they just had some textthey just had some textthey just had some textthey just had some textthey just had some textthey just had some textthey just had some text</p>
      </b-col>
    </b-row>
  </b-container>
</template>
<script>
export default {
  data () {
    return {
      mainProps: { blank: true, width: 75, height: 75, class: 'm1' }
    }
  }
}
</script>
<style scoped lang="scss">
</style>
