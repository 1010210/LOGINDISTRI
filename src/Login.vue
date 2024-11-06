<template>
  <div class="container">
    <h2>Login</h2>
    <form @submit="login">
      <div class="form-group">
        <label for="email">Email:</label>
        <input type="text" id="email" v-model="formData.email" />
      </div>
      <div class="form-group">
        <label for="password">Password:</label>
        <input type="password" id="password" v-model="formData.password" />
      </div>
      <div class="form-group">
        <button class="button button-primary" type="submit">Login</button>
      </div>
      <!-- Elemento para mostrar el mensaje de error -->
      <p v-if="error" class="error-message">{{ error }}</p>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      formData: {
        email: "",
        password: "",
      },
      error: null, // Inicialmente no hay error
    };
  },
  methods: {
    async login(event) {
      event.preventDefault();
      this.error = null; // Limpia cualquier error anterior

      try {
        const response = await fetch('https://tarea4login.netlify.app/.netlify/functions/login', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify(this.formData),
        });

        if (response.status === 200) {
          const data = await response.json();
          // Guarda el token en una cookie en lugar de localStorage
          document.cookie = `token=${data.token};path=/`;
          this.$router.push("/home");
        } else {
          // Muestra un mensaje de error cuando la contraseña es incorrecta
          this.error = 'Contraseña incorrecta';
        }
      } catch (error) {
        console.error('Error de autenticación:', error);
      }
    },
  },
};
</script>
