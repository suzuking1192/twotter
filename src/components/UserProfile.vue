<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@{{user.username}}</h1>
        <div class="user-profile__admin-badge" v-if="user.isAdmin">
          Admin
        </div>
      <div class="user-profile__follwer-count">
        <strong>Followers:</strong>{{followers}}
      </div>
      <form class='user_profile__create-twoot' @submit.prevent='createNewTwoot' :class="{'--exceeded': newTwootCharacterCount > 180}">
        <label for='newTwoot'>New twoot({{newTwootCharacterCount}}/180)</label>
        <textarea id='newTwoot' rows='4' v-model='newTwootContent'/>

        <div class="user-profile__create-twoot-type">
          <label for='newTwootType'>Type:</label>
          <select id='newTwootType' v-model='selectedTwootType'>
            <option :value='option.value' v-for='(option,index) in twootTypes' :key='index'>
              {{ option.name }}
            </option>
          </select>
        </div>

        <button>
          Twoot!
        </button>

      </form>
    </div>
    <div class="user-profile__twoots-wrapper">
      <TwootItem v-for="twoot in user.twoots" :key="twoot.id" :username="user.username" :twoot="twoot" @favorite="toggleFavorite" />
    </div>
  </div>

</template>

<script>
import TwootItem from "./Twootitem";


export default {
  name: 'UserProfile',
  components:{TwootItem},
  data(){
  return{
    newTwootContent:'',
    selectedTwootType:'instant',
    twootTypes:[
      {value:'draft',name:'Draft'},
      {value:'instant',name:'Instant twoot'},
    ],
    followers: 0,
    user:{
      id:1,
      username:"_yuto",
      firstname:"Yuto",
      lastname:"Suzuki",
      email:"mokkumokku99@gmail.com",
      isAdmin: true,
      twoots:[
        {id:1,content:"Twotter is amazing!"},
        {id:2, content:"Don't forget to subscribe our channels."},
      ]
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

    },
    newTwootCharacterCount(){
      return this.newTwootContent.length;
    }

  },
  methods:{
    followUser(){
       this.followers++;
    },
    toggleFavorite(id){
      console.log(`Favorited Twoot #${id}`);
    },
    createNewTwoot(){
      if (this.newTwootContent  && this.selectedTwootType !== 'draft'){
        this.user.twoots.unshift( {
          id: this.user.twoots.length + 1 ,
          content: this.newTwootContent,
        })
        this.newTwootContent=''
      }
    }
  },

  mounted(){
    this.followUser();

  }
}
</script>

<style lang='scss' scoped>
.user-profile{
  display:grid;
  grid-template-columns: 1fr 3fr;
  width: 100%;
  padding: 50px 5%;

  .user-profile__user-panel{
    display:flex;
    flex-direction:column;
    margin-right: 50px;
    padding:20px;
    background-color:white;
    border-radius: 5px;
    border:1px solid #DFE3E8;
  }

  h1{
    margin:0;
  }

  .user-profile__admin-badge{
    background: red;
    color: white;
    border-radius: 5px;
    margin-right:auto;
    padding:0 10px;
    font-weight: bold;
  }

  .user_profile__create-twoot{
    border:1px solid #DFE3E8;
    display: flex;
    padding-top: 20px;
    flex-direction:column;

    &.--exceeded{
      color:red;
    }
  }

}




</style>
