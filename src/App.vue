<template>
  <div class="register" v-if="!registered">
    <RegisterForm/>
  </div>
  <div v-else class="tweetBox">
    <h2>Welcomjjgje {{ userData.name }}, write your first tweet</h2>
  </div>
  
</template>

<script>
import RegisterForm from './components/RegisterForm.vue'

export default {
  name: 'App',
  data() {
    return {
      userData : {},
      registered: false
    }
  },
  components: {
    RegisterForm
  },
  created() {
    console.log("hib");
      if(localStorage.getItem("tweet_registered") === 'true') {
        this.registered = true;
      }
      if(localStorage.getItem("tweet_registered_user")) {
          this.userData = JSON.parse(localStorage.getItem("tweet_registered_user"));
      }
  }
}
</script>
