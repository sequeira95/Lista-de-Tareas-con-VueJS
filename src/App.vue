<template>
  <v-app>
    <div>
      <NavBar></NavBar>
      <v-main>
        <router-view/>
      </v-main>
    </div>
  </v-app>
</template>

<script>
import NavBar from './components/NavBar.vue';

export default {
  name: 'App',
  components:{
    NavBar
},

  data: () => ({
    //
  }),
};
</script>
