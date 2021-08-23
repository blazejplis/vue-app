<template>
  <div class="home">
        <h1>Home</h1>
        <div class="users-list">

            <router-link v-for="user in users" :to="{ name:'UserProfile', params: {userId: user.id}  }" :key="user.id" >

                {{user.username}}
                
            </router-link>

            <h1>Most recent Twoots</h1>
                    

        </div>

  </div>
</template>

<script>
import {users} from '../assets/users';

export default {
  name: 'Home',
  setup(){
    return{
        users
    }
  }
}
</script>

<style scoped lang="scss">
.home{
  padding: 50px;
  color: #f2e7fe;
}

</style>