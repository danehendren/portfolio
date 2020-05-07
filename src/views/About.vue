<template>
  <div class="about">
    <h1>This is an about page</h1>
    <img alt="Vue logo" src="../assets/dane.jpg">
    <div>
      <b-img src="../assets/dane.jpg" v-bind="mainProps" rounded="circle" alt="Circle image"></b-img>
    </div>
  </div>
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
