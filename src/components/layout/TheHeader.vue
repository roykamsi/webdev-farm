<template>
  <header>
    <nav>
      <h1 class="logo">
        <router-link to="/">Web Dev Farm</router-link>
      </h1>
      <ul>
        <li>
          <router-link to="/devs">All Devs</router-link>
        </li>
        <li v-if="isLoggedin">
          <router-link to="/requests">Requests</router-link>
        </li>
        <li v-if="!isLoggedin">
          <router-link to="/auth">Login</router-link>
        </li>
        <li v-if="isLoggedin">
          <base-button @click="logout">Logout</base-button>
        </li>
      </ul>
    </nav>
  </header>
</template>

<script>
export default {
  computed: {
    isLoggedin() {
      const logCheck = this.$store.getters.isAuthenticated;
      return logCheck;
    },
  },
  methods: {
    logout() {
      this.$store.dispatch('logout');
      this.$router.replace('/devs');
    },
  },
};
</script>

<style scoped>
header {
  width: 100%;
  height: 5rem;
  background-color: #0C1847;
  display: flex;
  justify-content: center;
  align-items: center;
}

header a {
  text-decoration: none;
  color: #dbbfa5;
  display: inline-block;
  padding: 0.75rem 1.5rem;
  border: 1px solid transparent;
}

a:active,
a:hover,
a.router-link-active {
  border: 1px solid #dbbfa5;
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

@media only screen and (max-width: 767px) {
  .logo {
    padding: .5rem;
  }
  header {
    height: auto;
    padding: 0;
  }
  header nav {
    width: 100%;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    margin-bottom: 2rem;
  }
  input {
    padding: 1rem;
  }
  li {
    padding: 0rem;
    border: none;
  }
}
</style>
