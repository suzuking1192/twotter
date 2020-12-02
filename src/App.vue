<template>
  <div id="app">
    {{user.username}}-{{fullName}}
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

  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
