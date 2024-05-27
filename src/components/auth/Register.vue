<template>
    <div class="container mx-auto">
      <div class="max-w-md mx-auto mt-10">
        <h2 class="text-2xl mb-4">Register</h2>
        <form @submit.prevent="handleRegister">
          <div class="mb-4">
            <label class="block">Frist name</label>
            <input type="text" v-model="firstName" class="w-full px-3 py-2 border rounded" />
          </div>
          <div class="mb-4">
            <label class="block">Last name</label>
            <input type="text" v-model="lastName" class="w-full px-3 py-2 border rounded" />
          </div>
          <div class="mb-4">
            <label class="block">Phone number</label>
            <input type="text" v-model="phoneNumber" class="w-full px-3 py-2 border rounded" />
          </div>
          <div class="mb-4">
            <label class="block">Email</label>
            <input type="email" v-model="email" class="w-full px-3 py-2 border rounded" />
          </div>
          <div class="mb-4">
            <label class="block">Password</label>
            <input type="password" v-model="password" class="w-full px-3 py-2 border rounded" />
          </div>
          <button type="submit" class="w-full bg-blue-500 text-white py-2 rounded">Register</button>
        </form>
      </div>
    </div>
  </template>
  
  <script>
  import AuthService from '@/services/auth.service';
  
  export default {
    data() {
      return {
        firstName: '',
        lastName: '',
        phoneNumber: '',
        email: '',
        password: ''
      };
    },
    methods: {
      handleRegister() {
        AuthService.register({ firstName: this.firstName, lastName: this.lastName, phoneNumber: this.phoneNumber, email: this.email, password: this.password })
          .then(() => {
            this.$router.push('/login');
          })
          .catch(error => {
            console.error(error);
          });
      }
    }
  };
  </script>