<template>
  <v-app>
    <div id="heading">
          <img style="margin-top: -50px" class="image" width="300" height="300" src="./assets/bookLogo.png">
          <h1> Book Looker </h1>
      </div>

     <home id="home" />

    
  </v-app>
</template>

<script>

import home from './components/home.vue'

export default {
  name: 'App',

  components: {
    home
  },

};
</script>

<style>

#heading{
  text-align: center
  
  
}


h1{
  margin-top: -70px;
  color: black;
  font-weight: 600;

}

#home{
  padding-top: 50px;
}


</style>
