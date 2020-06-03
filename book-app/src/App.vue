<template>
  <v-app>


      <div id="content">

        <v-flex v-if="currentPage == 'Home'" sm10>
            <v-btn text large color="#00b9be">Home</v-btn>
            <v-btn text large v-on:click="currentPage = 'ISBN'">ISBN Gen</v-btn>
        </v-flex>

        <v-flex v-if="currentPage == 'ISBN'" sm10>
            <v-btn text large v-on:click="currentPage = 'Home'">Home</v-btn>
            <v-btn text large color="#00b9be">ISBN Gen</v-btn>
        </v-flex>

      <home v-if="currentPage == 'Home'" id="home" />
      <isbn v-if="currentPage == 'ISBN'" id="isbn" />
      </div>

    
    
  </v-app>
</template>

<script>



import home from './components/home.vue'
import isbn from './components/isbn.vue'

export default {
  name: 'App',

  components: {
    home,
    isbn
  },

  data () {
    return {
      currentPage: "Home",
    }
  },
  methods: {

    isValidISBN: function(number_to_test) {
      let sum = 0;
      let num = number_to_test.toString().split("-").join("");
      if (num.length !== 10 && num.length !== 13) {
        return false;
      }
      if (isNaN(num.replace("X", "0"))) {
        return false;
      }

      let x = 0;
      for (var i = num.length; i > 0; i--) {
        if (num[x] == "X") {
          sum = sum + (i * 10);
        }
        else {
          sum = sum + (i * parseInt(num[x]));
        }
        x++;
      }

      return (sum % 11 === 0);
    },


  },

};
</script>

<style>





</style>
