<template>
  <div id="app">
    <nav class="bg-gray-800 p-4">
      <div class="flex justify-between items-center">
        <a href="/" class="text-white text-lg font-bold">Startup vue</a>
        <div class="flex space-x-4">
          <router-link to="/home" class="text-gray-300 hover:text-white">
            <font-awesome-icon icon="home" /> Home
          </router-link>
          <router-link v-if="showAdminBoard" to="/admin" class="text-gray-300 hover:text-white">
            Admin Board
          </router-link>
          <router-link v-if="showModeratorBoard" to="/mod" class="text-gray-300 hover:text-white">
            Moderator Board
          </router-link>
          <router-link v-if="currentUser" to="/user" class="text-gray-300 hover:text-white">
            User
          </router-link>
        </div>

        <div class="flex space-x-4">
          <div v-if="!currentUser" class="flex space-x-4">
            <router-link to="/register" class="text-gray-300 hover:text-white">
              <font-awesome-icon icon="user-plus" /> Sign Up
            </router-link>
            <router-link to="/login" class="text-gray-300 hover:text-white">
              <font-awesome-icon icon="sign-in-alt" /> Login
            </router-link>
          </div>

          <div v-if="currentUser" class="flex space-x-4">
            <router-link to="/profile" class="text-gray-300 hover:text-white">
              <font-awesome-icon icon="user" />
              {{ currentUser.username }}
            </router-link>
            <a class="text-gray-300 hover:text-white cursor-pointer" @click.prevent="logOut">
              <font-awesome-icon icon="sign-out-alt" /> LogOut
            </a>
          </div>
        </div>
      </div>
    </nav>

    <div class="container mx-auto mt-4">
      <router-view />
    </div>
  </div>
</template>

<script>
export default {
  computed: {
    currentUser() {
      return this.$store.state.auth.user;
    },
    showAdminBoard() {
      if (this.currentUser && this.currentUser['roles']) {
        return this.currentUser['roles'].includes('ROLE_ADMIN');
      }

      return false;
    },
    showModeratorBoard() {
      if (this.currentUser && this.currentUser['roles']) {
        return this.currentUser['roles'].includes('ROLE_MODERATOR');
      }

      return false;
    }
  },
  methods: {
    logOut() {
      this.$store.dispatch('auth/logout');
      this.$router.push('/login');
    }
  }
};
</script>