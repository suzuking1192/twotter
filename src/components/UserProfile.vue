<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@{{user.username}}</h1>
      <div class="user-profile__follwer-count">
        <strong>Followers:</strong>{{followers}}
      </div>
    </div>
  </div>

</template>

<script>

export default {
  name: 'App',
  data(){
  return{
    followers: 0,
    user:{
      id:1,
      username:"_yuto",
      firstname:"Yuto",
      lastname:"Suzuki",
      email:"mokkumokku99@gmail.com",
      isAdmin: true
      }
    }
  },
  watch:{
    followers(newFollowerCount, oldFollowerCount){
      if (oldFollowerCount < newFollowerCount){
        console.log(`${this.user.username} has gained a follower!`)
      }
    }
  },
  computed:{
    fullName(){
        return `${this.user.firstname} ${this.user.lastname}`;

    }

  },
  methods:{
    followUser(){
       this.followers++;
    }
  },

  mounted(){
    this.followUser();

  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: flex;
  color: #2c3e50;
  flex-direction: column;
  text-align:center;
}
</style>
