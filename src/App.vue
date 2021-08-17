<template>
  <nav>
    <div class="logo"><h2>Twotter</h2></div>
    <div><h3>@{{ state.user.username }}</h3></div>
  </nav>
  <router-view/>
</template>

<script>
import { reactive } from 'vue';

export default {
  name: 'App',
  setup(){
    const state = reactive({
        user: {
          username: 'blazejplis'
        }
    })
    return{
      state
    }
  }
}
</script>


<style lang="scss" >

  body{
    min-height: 100vh;
  }

</style>
