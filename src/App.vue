<template>
  <div class="app-container">

    <!-- Show logo only on specific pages -->
    <img v-if="showLogo" alt="Rest logo" src="./assets/rest.jpg" class="logo">
    <router-view></router-view>

  </div>
</template>


<script>



export default {
  name: 'App',
  components: {

  },
  computed: {
    showLogo() {
      return this.$route.name === "Login" || this.$route.name === "SignUp";
    }
  }
}
</script>
