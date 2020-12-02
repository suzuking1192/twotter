<template>
  <div id="app">
    {{user.username}}-{{fullName}}
    <strong>Followers:</strong>{{followers}}
    <button @click='followUser'>
      Follow
    </button>
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
