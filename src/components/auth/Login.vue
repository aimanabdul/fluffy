<template>
    <div class="container mx-auto">
      <div class="max-w-md mx-auto mt-10">
        <h2 class="text-2xl mb-4">Login</h2>
        <form @submit.prevent="handleLogin">
          <div class="mb-4">
            <label class="block">Username</label>
            <input type="text" v-model="username" class="w-full px-3 py-2 border rounded" />
          </div>
          <div class="mb-4">
            <label class="block">Password</label>
            <input type="password" v-model="password" class="w-full px-3 py-2 border rounded" />
          </div>
          <button type="submit" class="w-full bg-blue-500 text-white py-2 rounded">Login</button>
        </form>
      </div>
    </div>
  </template>
  
  <script>
  import AuthService from '@/services/auth.service';
  
  export default {
    data() {
      return {
        username: '',
        password: ''
      };
    },
    methods: {
      handleLogin() {
        AuthService.login({ username: this.username, password: this.password })
          .then(() => {
            this.$router.push('/profile');
          })
          .catch(error => {
            console.error(error);
          });
      }
    }
  };
  </script>
  