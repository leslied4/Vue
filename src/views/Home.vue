<template>
  <div class="home">
    <h1>Home</h1>
    <div class="users-list">
      <router-link 
        v-for="user in users" 
        :key="user.id" 
        :to="{ name: 'UserProfile', params: { userId: user.id - 1} }"
      >
        {{ user.username }}
      </router-link>
    </div>
  </div>

</template>

<script>
import { users } from "@/assets/users.js";
export default {
  name: 'Home',
  data() {
    return {
      users: users
    }
  }
}
</script>

<style lang="scss" scoped>
  .home {
    padding: 50px 5%;
    .users-list {
      display: flex;
      flex-direction: column;
    }
  }
</style>
