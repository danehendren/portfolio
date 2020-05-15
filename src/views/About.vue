<template>
  <b-container>
    <b-row align-v="center" align-h="center">
      <div class="about">
        <!-- <h1 class="mt-3">Optional Title</h1> -->
        <b-img alt="Profile Image" class="profile mt-5" fluid rounded="circle" thumbnail :src="require('../assets/tester.jpg')"></b-img>
        <div class="m-3">
          <h1>Irina Schaefer</h1>
          <p class="mx-auto about-description" style="max-width: 800px;">Contrary to popular belief, Lorem Ipsum is not simply random text. It has roots in a piece of classical Latin literature from 45 BC, making it over 2000 years old. Richard McClintock, a Latin professor at Hampden-Sydney College in Virginia, looked up one of the more obscure Latin words, consectetur, from a Lorem Ipsum passage, and going through the cites of the word in classical literature, discovered the undoubtable source.</p>
          <br>
          <p class="mx-auto about-description" style="max-width: 800px;">Contrary to popular belief, Lorem Ipsum is not simply random text. It has roots in a piece of classical Latin literature from 45 BC, making it over 2000 years old. Richard McClintock, a Latin professor at Hampden-Sydney College in Virginia, looked up one of the more obscure Latin words, consectetur, from a Lorem Ipsum passage, and going through the cites of the word in classical literature, discovered the undoubtable source.</p>
        </div>
      </div>
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
.profile{
  height: auto;
  width: 50%;
}
.about-description{
  line-height: 2.50rem;
  font-size: 1.50rem;
}
</style>
