<template>
    <b-row noGutters>
      <div class="about">
        <b-img alt="Profile Image" class="profile mt-5" fluid rounded="Rounded image" thumbnail :src="require('../assets/foxsit.jpg')"></b-img>
        <div class="m-3">
          <!-- <h1 v-on:click="emailMe">Email Me</h1> -->
          <b-button v-b-tooltip.hover.right="'Clicking will open your email client'" variant="outline-success" v-on:click="emailMe">Click To Email Me</b-button>
          <p class="mx-auto about-description" style="max-width: 800px;">Contrary to popular belief, Lorem Ipsum is not simply random text. It has roots in a piece of classical Latin literature from 45 BC, making it over 2000 years old. Richard McClintock, a Latin professor at Hampden-Sydney College in Virginia, looked up one of the more obscure Latin words, consectetur, from a Lorem Ipsum passage, and going through the cites of the word in classical literature, discovered the undoubtable source.</p>
        </div>
      </div>
    </b-row>
</template>

<script>
export default {
  name: 'Contact',
  data () {
    return {
      mainProps: { blank: true, width: 75, height: 75, class: 'm1' }
    }
  },
  methods: {
    emailMe: function () {
      window.location.href = 'mailto:irinaschaefer.4@gmx.de'
    }
  }
}
// Regular expression from W3C HTML5.2 input specification:
// https://www.w3.org/TR/html/sec-forms.html#email-state-typeemail
</script>
<style scoped lang="scss">
.profile{
  height: auto;
  width: 30%;
}
.about-description{
  line-height: 2.50rem;
  font-size: 1.50rem;
}
</style>
