<template>
    <div class="container mx-auto">
      <div class="max-w-md mx-auto mt-10">
        <h2 class="text-2xl mb-4">Moderator Board</h2>
        <p v-if="content">{{ content }}</p>
      </div>
    </div>
  </template>
  
  <script>
  import UserService from '@/services/test.service';
  
  export default {
    data() {
      return {
        content: ''
      };
    },
    mounted() {
      UserService.getModeratorBoard().then(response => {
        this.content = response.data;
      }).catch(error => {
        console.error(error);
      });
    }
  };
  </script>
  