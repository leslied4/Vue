<template>
  <nav>
    <router-link to="/" class="logo">
      <div>
        <strong>Twitter</strong>
      </div>
    </router-link>
    <div class="user" v-if="user">
      @<strong>{{ user.username }}</strong>
    </div>
  </nav>
  <router-view/>
</template>

<script>
import { useStore } from "vuex";
export default {
  name: 'App',
  data() {
    return {
      store: useStore()
    }
  },
  computed: {
    user() {
      return this.store.state.User.user;
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  background-color: #F3F5FA;
  min-height: 100vh;
}

nav {
  display: flex;
  justify-content: space-between;
  background: rgb(241, 131, 151);
  height: 8vh;
  align-items: center;

  .logo {
    font-weight: bold;
    color: white;
    width: 10%;
    display: flex;
    justify-content: center;
  }
  .user {
    font-weight: bold;
    width: 10%;
    text-align: center;
    color: white;
  }
}

</style>
