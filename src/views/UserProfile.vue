<template>

  <div class="user-profile">
    <div class="user-panel">
      <div class="panel-info">
        <h1 class="username">@{{ user.username }}</h1>
        <div class="admin-badge" v-if="user.isAdmin">
          Admin
        </div>
        <div class="follower-count">
          <strong>Followers: </strong>{{ followers }}
        </div>
      </div>
      <CreateTweetPanel @add-tweet="addNewTweet"/>
    </div>
    <div class="tweets-wrapper">
      <Tweets 
        v-for="tweet in user.tweets" 
        :key="tweet.id" 
        :username="user.username" 
        :tweet="tweet" 
        @favorite="toggleFavorite" 
      />
  </div>
  </div>
</template>

<script>
import { useRoute } from "vue-router";
// import { reactive, computed } from "module";
import Tweets from "@/components/Tweets";
import { users } from "@/assets/users.js";
import CreateTweetPanel from "@/components/CreateTweetPanel";
export default {
  name: 'UserProfile',
  components: {
    Tweets,
    CreateTweetPanel
  },
  data() {
    return {
      newTweetContent: '',
      selectedTweetType: 'instant',
      tweetType: [
        { value: 'draft', name: 'Draft' },
        { value: 'instant', name: 'Instant Tweet' }
      ],
      followers: 0,
      route: useRoute(),
      user: users[useRoute().params.userId] || users[0]
    }
  },
  watch: {

  },
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`
    },
    newTweetCharacterCount() {
      return this.newTweetContent.length;
    },
    userId () {
      return this.route.params.userId;
    }
  },
  methods: {
    followUser() {
      this.followers++
    },
    addNewTweet(content) {
      this.user.tweets.unshift({
        id: this.user.tweets.length + 1,
        content: content
      })
    },
  },
  mounted() {
    this.followUser();
  }
}
</script>

<style lang="scss" scoped>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  padding: 20px;

  .tweets-wrapper {
    display: flex;
    flex-direction: column;
    grid-gap: 10px;
  }

  .panel-info {
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #DFE3E8;

    .admin-badge {
      background-color: rgb(241, 131, 151);
      padding: 5px;
      color: white;
      margin-right: auto;
      border-radius: 5px;
    }


    h1 {
      margin: 0%;
    }

    h2 {
      margin: 10px;
    }
  }
}



</style>