<template>
  <form class="create-tweet" @submit.prevent="createNewTweet" :class="{ '--exceeded': newTweetCharacterCount > 180 }">
    <label for="newTweet"><strong>New Tweet</strong>({{ newTweetCharacterCount }}/180)</label>
    <textarea name="" id="newTweet" rows="4" v-model="state.newTweetContent"/>
    <div class="submit">
      <div class="create-tweet-type">
        <label for="newTweetType"><strong>Type:</strong></label>
        <select name="" id="newTweetType" v-model="state.selectedTweetType">
          <option v-for="(option, index) in state.tweetType" :value="option.value" :key="index">
            {{ option.name }}
          </option>
        </select>
      </div>
      <button>
        Tweet It!
      </button>
    </div>
  </form>
</template>

<script>
import { reactive, computed } from "vue";
export default {
  name: 'CreateTweetPanel',
  setup(props, context) {
    const state =  reactive( {
      newTweetContent: '',
      selectedTweetType: 'instant',
      tweetType: [
        { value: 'draft', name: 'Draft' },
        { value: 'instant', name: 'Instant Tweet' }
      ]
    })

    const newTweetCharacterCount = computed(() => state.newTweetContent.length)

    function createNewTweet() {
      if (state.newTweetContent && state.selectedTweetType !== 'draft' && state.newTweetContent.length < 181) {
        context.emit('add-tweet', state.newTweetContent)
        state.newTweetContent = ''
      }
    }

    return {
      state,
      newTweetCharacterCount,
      createNewTweet
    }
  }
};
</script>

<style lang="scss" scoped>
  .create-tweet {
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding-top: 20px;

    &.--exceeded {
      color: red;
      border-color: red;


    }

    .submit {
      display: flex;
      justify-content: space-between;
      align-items: center;

      button {
        color: white;
        border: none;
        border-radius: 5px;
        color: white;
        background-color: rgb(241, 131, 151);
        padding: 5px;
        border-radius: 5px;
      }
    }
  }
</style>