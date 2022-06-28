<template>
  <header>
      <nav>
      <h1>
        <router-link to="/">
        <i class="fa-solid fa-user-astronaut"></i>
        Find a Coach</router-link>
      </h1>
      <ul>
        <li>
          <router-link to="/coaches">
          <i class="fa-solid fa-user-secret"></i>
          All Coaches</router-link>
        </li>
        <li v-if="isLoggedIn">
          <router-link to="/requests">
          <i class="fa-solid fa-circle-nodes"></i>
          Requests</router-link>
        </li>
        <li v-else>
          <router-link to="/auth">
         <i class="fa-solid fa-arrow-right-to-bracket"></i>
          Login</router-link>
        </li>
        <li v-if="isLoggedIn">
          <base-button @click="logout">
          <i class="fa-solid fa-person-running"></i>
          Logout</base-button>
        </li>
      </ul>
      </nav>
  </header>
</template>

<script>
import Swal from 'sweetalert2';

export default {
  components:[ Swal ] ,
  data(){
      return{
        logouttoast : false,
        logintoast : false
      }
  },
  computed: {
    isLoggedIn() {
      return this.$store.getters.isAuthenticated;
    }
  },
  methods: {
    logout() {
      this.$store.dispatch('logout');
      this.$router.replace('/coaches');
      Swal.fire({
  icon: 'success',
  title: 'Logged out',
  showConfirmButton: false,
  timer: 1500
})
    }
  }
}
</script>

<style scoped>
header {
  width: 100%;
  height: 5rem;
  background-color: #3d008d;
  display: flex;
  justify-content: center;
  align-items: center;
}

header a {
  text-decoration: none;
  color: #ffffff;
  display: inline-block;
  padding: 0.75rem 1.5rem;
  border: 1px solid transparent;
}

a:active,
a:hover,
a.router-link-active {
  border: 1px solid gray;
}

h1 {
  margin: 0;
}

h1 a {
  color: white;
  margin: 0;
}

h1 a:hover,
h1 a:active,
h1 a.router-link-active {
  border-color: transparent;
}

header nav {
  width: 90%;
  margin: auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

header ul {
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
}

li {
  margin: 0 0.5rem;
}
</style>