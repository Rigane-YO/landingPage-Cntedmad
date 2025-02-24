<template>
    <div class="container-fluid min-vh-100 d-flex align-items-center justify-content-center bg-light">
      <div class="card shadow-lg" style="max-width: 400px; width: 100%;">
        <div class="card-body p-5">
          <div class="text-center mb-4">
            <Logo />
            <h2 class="fw-bold">Connexion</h2>
          </div>
          
          <form @submit.prevent="handleLogin">
            <div class="mb-3">
              <label for="email" class="form-label">Email</label>
              <input 
                type="email" 
                class="form-control" 
                id="email" 
                v-model="email"
                :class="{ 'is-invalid': validationErrors.email }"
                required
              >
            </div>
            
            <div class="mb-3">
              <label for="password" class="form-label">Mot de passe</label>
              <input 
                type="password" 
                class="form-control" 
                id="password" 
                v-model="password"
                :class="{ 'is-invalid': validationErrors.password }"
                required
              >
            </div>
            
            <div class="mb-3 text-end">
              <a href="#" class="text-decoration-none">Mot de passe oublié ?</a>
            </div>
            
            <button type="submit" class="btn btn-primary w-100 mb-3">
              Se connecter
            </button>
            
            <div class="text-center">
              <router-link to="/register" class="text-decoration-none">
                Pas encore de compte ? S'inscrire
              </router-link>
            </div>
          </form>
        </div>
      </div>
    </div>
  </template>
  
  <script setup lang="ts">
  import { ref } from 'vue'
  import Logo from '../components/Logo.vue'
  
  const email = ref('')
  const password = ref('')
  const validationErrors = ref({
    email: false,
    password: false
  })
  
  const handleLogin = () => {
    validationErrors.value.email = !email.value
    validationErrors.value.password = !password.value
    
    if (!validationErrors.value.email && !validationErrors.value.password) {
      console.log('Login attempt:', { email: email.value, password: password.value })
    }
  }
  </script>