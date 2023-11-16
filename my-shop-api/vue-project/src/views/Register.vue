<template>
  <div class="register-container">
      <h1>S'inscrire</h1>
      <p class="register_subtile"> J'ai déjà un compte,<RouterLink to="/login"> Me connecter </RouterLink></p>
      <form class="register-form" @submit.prevent="register">
        <label for="email">Email:</label>
      <input v-model="email" type="text" id="email" required>
        <label for="fullname">Nom d'utilisateur:</label>
        <input v-model="fullname" type="text" id="fullname" required>
  
        <label for="password">Mot de passe:</label>
        <input v-model="password" type="password" id="password" required>
  
        <label for="confirmPassword">Confirmer le mot de passe:</label>
        <input v-model="confirmPassword" type="password" id="confirmPassword" required>
  
        <button type="submit">S'inscrire</button>
      </form>
    </div>
  </template>
  
  <script scoped>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        email: '', 
        fullname: '',
        password: '',
        confirmPassword: '',
      };
    },
    methods: {
      async register() {
        try {
          if (this.password !== this.confirmPassword) {
            console.log('Les mots de passe ne correspondent pas.');
            return;
          }
  
          const authToken = "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpYXQiOjE3MDAxNDc3MTAsImV4cCI6MTcwMDE1MTMxMCwicm9sZXMiOlsiUk9MRV9BRE1JTiIsIlJPTEVfVVNFUiJdLCJ1c2VybmFtZSI6Ik5pbmhvMjI1QGdtYWlsLmNvbSJ9.sxtfcjD6NV3ZdqElUjr1LKK57cll4eK8w6_ONtQI03FrSz-vUfhiEpuhtFyevL3mSHHIlovCUMntKuU7PFWJ8nJFL6z6USd9ajBFSBeZ4G1veM0f0PdYmukxTsDMC9uludUkgyxcqMBR1D9fVe3-qXVlEaN8CqZPEHQxe0E7BvrMdZ0sJBLsf7FLvfDEzOrHQwB-lv_PjtHxrmOHFRTc8JOgA1AM1nGiMQyuwTuCpQfqpGnO1dofVKH9wvc4-XaTYaGU3fMxyMMrWO16hvquzSuWGe5QkQScuZ6r2vODgNQ1AYbyeAdfJUr4WRIJFf3PufmUEYAIgEiHWjNKQjgLAg"
  
          const response = await axios.post(
            'http://localhost/api/users',
            {
              fullname: this.fullname,
              password: this.password,
              email: this.email, 
            },
            {
              headers: {
                'Authorization': `Bearer ${authToken}`
              }
            }
          );
  
          console.log('Inscription réussie', response.data);
        } catch (error) {
          console.log('Erreur d\'inscription', error);
        }
      },
    },
  }
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