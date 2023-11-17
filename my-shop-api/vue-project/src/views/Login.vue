<template>
  <section class="login">
    <div class="login-container">
      <h1 class="login_title">Connexion</h1>
      <p class="login_subtile">
        Tu n'as pas encore de compte ?
        <RouterLink to="/register">Créer un compte</RouterLink>
      </p>
      <form class="login-form" @submit.prevent="login">
        <label for="username">E-mail</label>
        <input v-model="email" type="text" id="username" required />

        <label for="password">Mot de passe:</label>
        <input v-model="password" type="password" id="password" required />

        <button type="submit">Se connecter</button>
      </form>
    </div>
  </section>
</template>

<script scoped>
import router from "../router";

export default {
  data() {
    return {
      email: "",
      password: "",
      error: null,
    };
  },
  methods: {
    async login(email, password) {
      try {
        const response = await fetch("http://localhost/authentication_token", {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify({
            email: this.email,
            password: this.password,
          }),
        });

        if (!response.ok) {
          throw new Error("Erreur de connexion");
        }

        const data = await response.json();
        console.log("Connexion réussie", data);
        this.$router.push({ name: "home" });
      } catch (error) {
        console.error(error);
        this.error = "Identifiants invalides. Veuillez réessayer.";
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
