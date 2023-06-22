<template>
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
      registerAccount( ) {
    
        if(this.name !== "" && this.email !== "" && this.password !== "") {
            this.userData.name = this.name;
            this.userData.email = this.email;
            this.userData.id = ++this.userID;
            this.userData.password = this.password;
        } else {
            this.error = "Please fill in all the required fields."
        }

        localStorage.setItem("tweet_registered", true);
        localStorage.setItem("tweet_registered_user", JSON.stringify(this.userData));

        this.name = "";
        this.email = "";
        this.password = "";
        this.$emit('registered');
      }
    }
  };
  </script>
  
  