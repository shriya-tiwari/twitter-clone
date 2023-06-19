<template>
    <div class="card">
      <i class="fab fa-twitter fa-lg fa-fw"></i>

        <div class="register" v-if="!registered">
            <h2>Create your account</h2>
            <form @submit.prevent="registerAccount" id="register">
                <div class="form-group">
                <label for="name">Name 
                    <span>{{ name.length + '/' + max_length }}</span>
                </label>
                <input type="text" id="name" v-model="name" :maxLength="max_length" required>
                </div>
                <div class="form-group">
                <label for="email">Email
                    <span>{{ email.length + '/' + max_length }}</span>
                </label>
                <input type="email" id="email" v-model="email" :maxLength="max_length" required>
                </div>
                <div class="form-group">
                <label for="password">Password
                    <span>{{ password.length + '/' + max_pass_length }}</span>
                </label>
                <input type="password" id="password" v-model="password" :maxLength="max_pass_length" required>
                </div>
                <button type="submit">Register</button>
            </form>
            <div v-if="error.length > 0">{{ error }}</div>
        </div>
        
        <div v-else class="tweetBox">
            <h2>`Welcome ${this.name}, write your first tweet`</h2>
        </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        userData: {},
        name: "",
        email: "",
        password: "",
        max_length: 25,
        max_pass_length: 16,
        error: "",
        userID: 0,
        registered: false
      };
    },
    methods: {
      registerAccountt( ) {
    
        if(this.name !== "" && this.email !== "" && this.password !== "") {
            this.userData.name = this.name;
            this.userData.email = this.email;
            this.userData.id = ++this.userID;
            this.userData.password = this.password;
        } else {
            this.error = "Please fill in all the required fields."
        }

        localStorage.setItem("tweet_registered", true);
        localStorage.setItem("tweet_registererd_user", JSON.stringify(this.userData));

        this.name = "";
        this.email = "";
        this.password = "";
      },

      created() {
        console.log("hi");
        if(localStorage.getItem("tweet_registered") === 'true') {
            this.registered = true;
        }
        if(localStorage.getItem("tweet_registered_user")) {
            this.userData = JSON.parse(localStorage.getItem("tweet_registered_user"))
        }
      }
    }
  };
  </script>
  
  