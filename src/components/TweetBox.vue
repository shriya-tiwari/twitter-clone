<template>
    <h2>Welcome @{{ userData.name }}! <br> Share your thoughts and ideas in a tweet and let your voice be heard.</h2>
    <form @submit.prevent="sendTweet">
        <div class="tweet-form-group">
            <label for="tweet">
                Send your tweet
                <span> {{ tweetMsg.length + '/' + max_tweet }}</span>
            </label>
            <textarea name="tweet" id="tweet" cols="30" rows="10" v-model="tweetMsg" :maxlength="max_tweet"></textarea>
        </div>
        <button type="submit">Tweet</button>
    </form>
    <div class="card_tweets">
        <section class="tweets" v-if="tweets.length > 0">
            <h2>Tweets</h2>
            <div class="tweetMsg" v-for="(tweet, index) in tweets">
                <p>
                    {{tweet.text}}
                </p>

                <div class="tweetDate">
                    <i class="fas fa-calendar-alt fa-sm fa-fw"></i>{{tweet.date}}
                </div>
                <div class="tweet_remove" @click="openConfirm(index)">
                    <span class="remove">Delete this tweet <i class="fas fa-trash fa-xs fa-fw"></i></span>
                </div>
                <DeleteConfirm :is-open="isDeleteOpen" @cancel="cancelDelete" @confirm="confirmDelete(index)"></DeleteConfirm>
 
            </div>

        </section>
        <div v-else><h3>No tweets to show</h3></div>
    </div>
</template>
  
<script>
import DeleteConfirm from './DeleteConfirm.vue';

export default {
    data() {
        return {
            userData: {},
            usersID: 0,
            max_tweet: 500,
            error: "",
            tweetMsg: "", 
            tweets: [],
            tweetMsg: "",
            isDeleteOpen: false,
        };
    },
    components: {
        DeleteConfirm
    },
    created() {
        if(localStorage.getItem("tweet_registered_user")) {
            this.userData = JSON.parse(localStorage.getItem("tweet_registered_user"));
            console.log(this.userData.name);
        }
        if (localStorage.getItem("stored_tweets")) {
            console.log("There is a list of tweets");
            this.tweets = JSON.parse(localStorage.getItem("stored_tweets"));
        }
        else {
            console.log("No tweets here");
        } 
        
    },
    methods: {
        sendTweet() {
            this.tweets.unshift({
                text: this.tweetMsg,
                date: new Date().toLocaleTimeString()
            });
        
            this.tweetMsg = "";
            console.log(this.tweets);
            localStorage.setItem('stored_tweets', JSON.stringify(this.tweets));
        },
        openConfirm(index) {
            this.isDeleteOpen = true;
        },
        confirmDelete(index) {
            this.tweets.splice(index, 1);
            localStorage.stored_tweets = JSON.stringify(this.tweets);
            this.isDeleteOpen = false;
        },
        cancelDelete() {
            this.isDeleteOpen = false;
        },
    }
};
</script>
  
  