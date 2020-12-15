<template>
  <div class="tweet-item" @click="favoriteTweet(tweet.id)">
    <div class="tweet">
      <div class="user">
        @{{ username }}
      </div>
      <div class="content">
        {{ tweet.content }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Tweets',
  props: {
    username: {
      type: String,
      required: true
    },
    tweet: {
      type: Object,
      required: true
    }
  },
  methods: {
    favoriteTweet(id) {
      this.$emit('favorite', id)
    }
  }
}
</script>

<style lang="scss" scoped>
.tweet-item {
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #DFE3E8;
  box-sizing: border-box;
  cursor: pointer;
  transition: all 0.25s ease;
  margin-bottom: 1px;

  .user {
    font-weight: bold;
  }
  &:hover {
    transform: scale(1.04, 1.04);
  }
}



</style>