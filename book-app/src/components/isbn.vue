<template lang="html">

  <div id="home">

    
    <div id="heading">
      <div style="margin-top: 50px">
        <v-icon x-large color="#00b9be">fas fa-barcode</v-icon>
        <br>
        <span style="color: #436d6e; font-size:60%">156881111X</span>
      </div>
      <h1> ISBN Generator </h1>
      <h2>Generate new random 10 digit ISBN</h2>
    </div>

    <div style="text-align: center; margin-top: 20px">
      <v-btn v-on:click="generateISBN" color="#00b9be" medium dark>Generate New 
        <v-icon dark right>fas fa-plus-square</v-icon>
      </v-btn>

      <div v-for="(code, key) in codes" v-bind:key="key">
        <v-layout>
          <v-flex sm1> </v-flex>
          <v-flex sm5 class="list" v-text="code"></v-flex>
          <v-flex sm5 style="text-align: left; padding-top: 10px">
            <v-btn icon color="#00b9be" v-on:click="generateISBN">
              <v-icon>fas fa-copy</v-icon>
            </v-btn>
          </v-flex>
        </v-layout>
      </div>
    </div>



  </div>

</template>

<script lang="js">

  export default  {
    name: 'home',
    props: [],
    mounted () {

    },
    data () {
      return {
        codes: []
      }
    },
    methods: {

      generateISBN: function() {

        this.codes.push("7439478372")

        return;
      },

      

    },
    computed: {

    }
}


</script>


<style scoped>

h1{
  margin-top: 30px;
  color: black;
  font-weight: 600;
}

h2{
  text-align:center;
  color: teal;
  font-weight: 400;
  margin-top: 0px;  
}

#heading{
  left: 50%;  
  text-align: center;
  margin: 0 auto;
}

#main{
  padding-top: 40px;
}

.list{
  text-align: right;
  margin: auto;
  padding-top: 10px;
  padding-right: 5px;
  font-size: 140%;
}






</style>>




