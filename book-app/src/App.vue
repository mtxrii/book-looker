<template>
  <v-app>

    <div class="containter">
      <div id="heading">
            <img style="margin-top: -50px" class="image" width="300" height="300" src="./assets/bookLogo.png"> 
            <h1> Book Looker </h1>
            <h2>Search by ISBN, Author or Title</h2>
            
        </div>

      <div id="content">
      <home id="home" />
      </div>

    </div>
    
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
  
  left: 50%;  
  text-align: center;
  margin: 0 auto;
}



h2{
  text-align:center;
  color: teal;
  font-weight: 400;
  
  
}


h1{
  margin-top: -70px;
  color: black;
  font-weight: 600;

}





</style>
