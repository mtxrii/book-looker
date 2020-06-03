<template lang="html">

  <div id="home">

    <div id="main">
    
    <!-- container with searchbar and button -->
    <v-container fluid style="max-width: 700px" grid-list-md text-xs-center>
          <v-layout row wrap>
          <v-flex sm10>
            <v-text-field
                v-model = "searchField"
                dense
                label="Search"
                solo
              ></v-text-field>
          </v-flex>
          <v-flex sm2>
              <v-btn v-on:click="getRequest" color="#00b9be" medium dark>Search
              <v-icon dark right>fas fa-search</v-icon>
            </v-btn>
          </v-flex>
        </v-layout>
    </v-container>
    </div>

  <div class="list-group-item " style="margin-left: 1vw;  overflow-y: hidden; margin-right: 1vw; margin-bottom: 1vh; " v-for="(book, key) in titles" v-bind:key="key">

    <v-list-item-title
        style="word-break: normal; padding-top: 5px; display: inline-block; font-size: 18px; max-width:45vw"
        class=" text-truncate"
        text-truncate
        v-text = "book"
        
    > </v-list-item-title>
    
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
        title: false,
        author: false,
        isbn: false,
        data: "",
        titles: [],
        searchField: "",
        src: "",
      }
    },
    methods: {
      getRequest: function(){

        let splitString = this.searchField.split(" ");
        var url = "https://www.googleapis.com/books/v1/volumes?q=";
        for (let i=0; i<splitString.length; i++){
          url += splitString[i] + "+";
          if(i == splitString.length -1){
            url = url.substring(0, url.length - 1);
            url = url + "&maxResults=40"
          }
        }
        
        fetch(url)
        .then(data =>{return data.json()})
        .then(res=>{this.data = res; this.handleResponse()})
        
        // .catch(error=>this.data = "Nothing Found!");   
        
      },

      handleResponse: function() {
      console.log(this.data);
      this.titles = [];
      for (var i = 0; i < this.data.items.length; i++) {
        var item = this.data.items[i];
        this.titles.push(item.volumeInfo.title);
      }
    }

      

    },
    computed: {

    }
}


</script>


<style scoped>

h2{
  text-align:center;
  color: teal;
  font-weight: 400;
  margin-top: -40px;  
}

#home{
  padding-top: 50px;
  position: sticky;
  top: 0;
}


</style>>




