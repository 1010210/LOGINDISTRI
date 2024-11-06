<template>
  <div id="app" class="container">
    <div class="row" style="margin-top: 15px" v-if="!isLoginPage">
      <router-link class="three columns button button-primary" to="/Home">Home</router-link>
      <router-link class="three columns button button-primary" to="/book">Books</router-link>
      <router-link class="three columns button button-primary" to="/author">Authors</router-link>
      <router-link class="three columns button button-primary" to="/publisher">Publishers</router-link>
    </div>
    <router-view />
    <div class="row">
      <button disabled="disabled" class="twelve columns button-primary">
        Treicy León Tarea Login
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  computed: {
    isLoginPage() {
      return this.$route.path === "/login";
    },
  },
};
</script>
