<template>
  <div class="card">
      <i class="fab fa-twitter fa-lg fa-fw"></i>

      <div class="register" v-if="!registered">
        <RegisterForm @registered="handleRegistration"/>
      </div>
      <div v-else class="tweetBox">
        <TweetBox />
      </div>

  </div>
</template>

<script>
import RegisterForm from './components/RegisterForm.vue'
import TweetBox from './components/TweetBox.vue'

export default {
  name: 'App',
  data() {
    return {
      userData : {},
      registered: false
    }
  },
  components: {
    RegisterForm,
    TweetBox
  },
  methods :{
    handleRegistration() {
      this.registered = true;
    },
  },
  created() {
    console.log("hib");
    console.log(localStorage.getItem("tweet_registered"));
    if(localStorage.getItem("tweet_registered") === 'true') {
      this.registered = true;
    }
    if(localStorage.getItem("tweet_registered_user")) {
        this.userData = JSON.parse(localStorage.getItem("tweet_registered_user"));
        console.log(this.userData);
    }
  }
}
</script>
