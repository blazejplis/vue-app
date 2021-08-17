<template>
  <nav>
    <router-link to="/"><div class="logo"><h2>Twotter</h2></div></router-link>
    <div><h3 v-if="user">@{{ user.username }}</h3></div>
  </nav>
  <router-view/>
</template>

<script>
import { useStore } from 'vuex';
import { computed } from 'vue';

export default {
  name: 'App',
  setup(){
    const store = useStore();
    const user = computed(() => store.state.User.user)

    return{
      user
    }
  }
}
</script>


<style lang="scss" >

  body{
    min-height: 100vh;
  }

</style>
