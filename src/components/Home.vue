<template>
  <div>
    <h2 style="margin-top: 15px">
      Sitio de libros
      <button @click="logout" class="button button-primary" style="float: right">Logout</button>
    </h2>
    <p>Información sobre libros, autores y editores.</p>
    <ul>
      <li><router-link to='/book'>Books information</router-link></li>
      <li><router-link to='/author'>Authors information</router-link></li>
      <li><router-link to='/publisher'>Publishers information</router-link></li>
    </ul>
  </div>
</template>

<script>
export default {
  methods: {
    logout() {
      document.cookie = "token=; expires=Thu, 01 Jan 2000 00:00:00 UTC; path=/;";
      this.$router.push("/"); 
    },
  },
};
</script>
