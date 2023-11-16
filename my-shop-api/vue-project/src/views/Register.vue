<template>
<div class="register-container">
    <h1>S'inscrire</h1>
    <p class="register_subtile"> J'ai déjà un compte,<RouterLink to="/login"> Me connecter </RouterLink></p>
    <form class="register-form" @submit.prevent="register">
      <label for="username">Nom d'utilisateur:</label>
      <input v-model="username" type="text" id="username" required>

      <label for="password">Mot de passe:</label>
      <input v-model="password" type="password" id="password" required>

      <label for="confirmPassword">Confirmer le mot de passe:</label>
      <input v-model="confirmPassword" type="password" id="confirmPassword" required>

      <button type="submit">S'inscrire</button>
    </form>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      username: '',
      password: '',
      confirmPassword: '',
    };
  },
  methods: {
    async register() {
      try {
        if (this.password !== this.confirmPassword) {
          console.error('Les mots de passe ne correspondent pas.');
          return;
        }

        const response = await axios.post('URL_DE_VOTRE_API/register', {
          username: this.username,
          password: this.password,
        });

        console.log('Inscription réussie', response.data);
      } catch (error) {
        console.error('Erreur d\'inscription', error);
      }
    },
  },
};
</script>

<style>
.register-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 60vh;
  background-color: white;
  width: 100vw;
}

.register-form {
  width: 100%;
  max-width: 400px;
  padding: 20px;
  border: 1px solid #a4a0a0;
  background-color: #d1cfcf;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  margin-top: 16px;
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
  color: #fdfcfc;
  padding: 10px 15px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
h1 {
    color: black;
}
</style>