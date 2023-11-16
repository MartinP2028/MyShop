<template>
  <div class="login-container">
    <h1 class="login_title">Connexion</h1>
    <p class="login_subtile">
      Tu n'as pas encore de compte ?
      <RouterLink to="/register">Créer un compte</RouterLink>
    </p>
    <form class="login-form" @submit.prevent="login">
      <label for="username">Nom d'utilisateur:</label>
      <input v-model="username" type="text" id="username" required />

      <label for="password">Mot de passe:</label>
      <input v-model="password" type="password" id="password" required />

      <button type="submit">Se connecter</button>
    </form>
  </div>
</template>

<script scoped>
import axios from "axios";
import { RouterLink } from "vue-router";

export default {
  components: {
    RouterLink,
  },
  data() {
    return {
      username: "",
      password: "",
    };
  },
  methods: {
    async login() {
      try {
        const response = await axios.post("URL_DE_VOTRE_API/login", {
          username: this.username,
          password: this.password,
        });

        console.log("Connexion réussie", response.data);
      } catch (error) {
        console.error("Erreur de connexion", error);
      }
    },
  },
};
</script>

<style>
.login-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 60vh;
  background-color: white;
  width: 100vw;
}

.login-form {
  width: 100%;
  max-width: 400px;
  padding: 20px;
  border: 1px solid #a4a0a0;
  background-color: #d1cfcf;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

label {
  display: block;
  margin-bottom: 8px;
}

input {
  width: 100%;
  padding: 8px;
  margin-bottom: 16px;
  box-sizing: border-box;
}

button {
  background-color: #0a0e12;
  color: #fff;
  padding: 10px 15px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
h1 {
  color: black;
}
p {
  color: black;
}
</style>
