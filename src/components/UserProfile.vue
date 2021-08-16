<template>

  <div class="user-wrapper">
    <div class="user-card">
        <div class="user-card___details">
  <p v-if="user.isAdmin" class="user-card__admin-badge">Admin</p>
  <h1 class="user-card__username">@{{user.username}}</h1>
  <h2 class="user-card__full-name">{{ fullName }}</h2>
  
  <p class="user-card__followers"><strong>Followers:</strong> {{ followers }}</p>
        </div>
  <button v-on:click="followUser">Follow </button>
      <form class="user-card__new-twoot" @submit.prevent="createNewTwoot">
          <label for="new_twoot">Add new twoot</label>
          <textarea name="new_twoot" id="new_twoot" rows="4" v-model="newTwootContent "></textarea>
      
      <div class="user-card__create-twoot-type">
        <label for="twoot_type">Type: </label>
            <select name="twoot_type" id="twoot_type" v-model="selectedTwootType">
                <option :value="option.value" v-for="(option,index) in twootTypes" :key="index" >
                  {{ option.name }}
                  </option>   
            </select>
      </div>
      <button class="user-card__submit-twoot">Submit twoot</button>
      </form>
    </div>
    <div class="user-wrapper__twoots-wrapper">
        <TwootItem 
          v-for="twoot in user.twoots" 
          :key="twoot.id" 
          :username="user.username" 
          :twoot="twoot" 
          @favourite="toggleFavourite" 
        /> 
    </div>
  </div>
</template>

<script>
import TwootItem from "./TwootItem";

export default {
  name: 'UserProfile',
  components: { TwootItem },
  data(){
    return{
        newTwootContent: '',
        selectedTwootType: 'instant',
        twootTypes: [
          {value: 'draft', name: 'Draft'},
          {value: 'instant', name: 'Instant twoot'}
        ],
        followers: 0,
        user: {
          id: 1,
          username: 'blazejplis',
          firstName: 'Blazej',
          lastName: 'Plis',
          email: 'blazejplis@gmail.com',
          isAdmin: true,
          twoots: [
            {id: 1, content: "Twotter is amazing!"},
            {id: 2, content: "Everyhing is good!"}
          ]
        }
    }
  },
  watch: {
    followers(newFollowersCount, oldFollowersCount){
      if(oldFollowersCount < newFollowersCount){
        console.log(this.user.username + " has gained a new follower!")
      }
    }
  },
  computed: {
    fullName(){
      return this.user.firstName + " " + this.user.lastName;
    }
  },
  methods:{
    followUser(){
      this.followers++
    },
    toggleFavourite(id){
      console.log("Favourited! twoot #" + id);
    },
    createNewTwoot(){
      if(this.newTwootContent && this.selectedTwootType !== 'draft'){
          this.user.twoots.unshift({
            id: this.user.twoots.length + 1,
            content: this.newTwootContent
          })
      }
      this.newTwootContent = '';
    }
  },
  mounted(){
    this.followUser()
  }
}
</script>

<style lang="scss" scoped>
.user-wrapper {
  display: grid;
  grid-template-columns: 30vw 45vw;
  grid-gap: 1em;

  .user-wrapper__twoots-wrapper {
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    align-items: center;
  }

  .user-card {
    padding: 30px 50px;
    background-color: white;
    color: black;
    border-radius: 10px;
    font-family: Poppins;
    box-shadow: 0px 0px 10px 0px rgba(255, 255, 255, 0.6);
    height: 55vh;
    max-height: 55vh;

    h1,
    h2 {
      margin: 0;
    }

    h2 {
      opacity: 0.7;
    }

    .user-card__admin-badge {
      padding: 5px 10px;
      background-color: #f9844a;
      font-size: 0.9em;
      opacity: 0.8;
      color: white;
      border-radius: 5px;
    }

    .user-card button,
    .user-card__submit-twoot {
      background-color: #fec89a;
      text-transform: uppercase;
      border: none;
      border-radius: 5px;
      font-weight: 600;
      font-size: 0.9em;
      color: white;
      padding: 10px 25px;
      cursor: pointer;
      margin: 10px auto;
      width: 25%;
      text-align: center;
    }


    .user-card__submit-twoot {
      width: 100%;
      font-size: 1.1em;
      padding: 15px 30px;
    }

    .user-card___details {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: flex-start;
    }

    .user-card__new-twoot {
      padding-top: 20px;
      display: flex;
      flex-direction: column;
    }

    .user-card__new-twoot label,
    .user-card__create-twoot-type label {
      font-weight: 600;
    }

    .user-card__new-twoot textarea {
      font-family: Poppins;
      padding: 10px;
    }
  }
}
</style>