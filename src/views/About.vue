<template>
  <b-container>
    <b-row class="vh-100 text-center" align-v="center" align-h="center">
        <b-col cols="5">
          <b-img alt="#" :src="require('../assets/ph_photo.jpg')"></b-img>
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
