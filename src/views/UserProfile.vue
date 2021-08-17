<template>

  <div class="user-wrapper">
    <div class="user-card">
        <div class="user-card___details">
  <p v-if="state.user.isAdmin" class="user-card__admin-badge">Admin</p>
  <h1 class="user-card__username">@{{ state.user.username}}</h1>
  <h2 class="user-card__full-name">{{ state.fullName }}</h2>
  <h3>{{ userId }}</h3>
  
  <p class="user-card__followers"><strong>Followers:</strong> {{ state.followers }}</p>
        </div>
    <CreateTwootPanel
        @add-twoot="addNewTwoot"
     />
    </div>
    <div class="user-wrapper__twoots-wrapper">
        <TwootItem 
          v-for="twoot in state.user.twoots" 
          :key="twoot.id" 
          :username="state.user.username" 
          :twoot="twoot" 
        /> 
    </div>
  </div>
</template>

<script>
import { reactive, computed } from 'vue';
import { useRoute } from 'vue-router';
import TwootItem from "../components/TwootItem";
import CreateTwootPanel from "../components/CreateTwootPanel";

export default {
  name: 'UserProfile',
  components: { TwootItem, CreateTwootPanel },
  setup(){
      const route = useRoute();
      const userId = computed(() => route.params.userId)
      const state = reactive({
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
      })

      const fullName = computed(() => state.user.firstName + " " + state.user.lastName);

      function addNewTwoot(newContent){
        console.log(newContent)
          state.user.twoots.unshift({
            id: state.user.twoots.length + 1,
            content: newContent
          });
      }

      return{
        state,
        fullName,
        addNewTwoot,
        userId
      }
  }
};
</script>

<style lang="scss" >
.user-wrapper {
  display: flex;
  justify-content: space-around;
  width: 100%;
  padding: 5em;
  .user-card button,
  .user-card__submit-twoot {
    background-color: #bb86fc;
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
    color: white;
  }

  .user-wrapper__twoots-wrapper {
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    align-items: center;
    width: 35vw;
  }

  .user-card {
    padding: 30px 50px;
    background-color: #1e1e1e;
    color: #e1e1e1;
    border-radius: 10px;
    font-family: Poppins;
    box-shadow: 0px 0px 10px 0px rgba(0, 0, 0, 0.6);
    width: 30vw;
    max-height: 100%;
    overflow: hidden;
      align-self:flex-start;

    h1,
    h2 {
      margin: 0;
    }

    h2 {
      opacity: 0.7;
    }

    .user-card__admin-badge {
      padding: 5px 10px;
      background-color: #121212;
      font-size: 0.9em;
      opacity: 0.8;
      color: white;
      border-radius: 5px;
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

    form {
      .--exceeded {
        border: 2px solid red;

        &:focus {
          border: 2px solid red;
          outline: 2px solid red;
        }
      }

      >span {
        font-size: 0.7em;
        margin-bottom: 5px;
      }
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
      background-color: #534b5e;
      border-radius: 10px;
      outline: none;
      border: none;
      resize: vertical;
      border: 2px solid #534b5e;
      color: white;
      font-size: 0.9em;
      color: #e1e1e1;
      &:focus{
        border: 2px solid #bb86fc;
      }
    }
  }
}
</style>