<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@{{ user.username }}</h1>
      <div class="user-profile__admin-badge" v-if="user.isAdmin">
        Admin
      </div>
      <div class="user-profile__follower-count">
        <strong> Followers: </strong>{{ followers }}
      </div>
      <form class="user-profile__create-tweet">
        <label for="newTweet"><strong>New Tweet</strong></label>
        <textarea id="newTweet" rows="4"></textarea>
      </form>
    </div>

    <div class="user-profile_tweet-wrapper">
      <TweetItem
        v-for="tweet in user.tweet"
        :key="tweet.id"
        :username="user.username"
        :tweet="tweet"
        @favourite="toggleFavourite"
      />
    </div>
  </div>
</template>

<script>
import TweetItem from "./TweetItem.vue";

export default {
  components: { TweetItem },
  name: "UserProfile",
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: "Max",
        firstName: "Max",
        lastName: "B",
        email: "max@googlemail.com",
        isAdmin: false,
        tweet: [
          { id: 1, content: "tweeting is nice!" },
          { id: 2, content: "follow me!" },
        ],
      },
    };
  },
  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      if (oldFollowerCount < newFollowerCount) {
        console.log(`${this.user.username} has a new Follower`);
      }
    },
  },
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    },
  },
  methods: {
    followUser() {
      this.followers++;
    },
    toggleFavourite(id) {
      console.log(`Favourited Tweet #${id}`);
    },
  },
  mounted() {
    this.followUser();
  },
};
</script>

<style>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 100%;
  padding: 50px 5%;
}

.user-profile__user-panel {
  display: flex;
  flex-direction: column;
  margin-right: 50px;
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
}

.user-profile__admin-badge {
  -moz-box-align: center;
  background: rebeccapurple;
  color: white;
  border-radius: 5px;
  margin-right: auto;
  padding: 0 10px;
  font-weight: bold;
}

.user-profile__create-tweet {
  padding-top: 20xp;
  display: flex;
  grid-gap: column;
}

h1 {
  margin: 0;
}
</style>
