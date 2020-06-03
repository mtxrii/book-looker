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

  <div class="list-group-item " style="margin-left: 1vw;  overflow-y: hidden; margin-right: 1vw; margin-bottom: 1vh; " v-for="(book, key) in loopData" v-bind:key="key">

    <!-- <v-list-item-title
        style="word-break: normal; padding-top: 5px; display: inline-block; font-size: 18px; max-width:45vw"
        class=" text-truncate"
        text-truncate
        v-text = "book"
        
    > </v-list-item-title> -->


    <v-card
    class="mx-auto elevation-20"
    color="purple"
    dark
    style="max-width: 400px;"
  >
    <v-row justify="space-between">
      <v-col cols="8">
        <v-card-title primary-title>
          <div>
            <div v-text = "book.volumeInfo.title" class="headline"></div>
            <div v-text = "book.volumeInfo.authors"></div>
            <div v-text = "book.volumeInfo.publishedDate"></div>
          </div>
        </v-card-title>
      </v-col>
      <v-img
        class="shrink ma-2"
        contain
        src="book.volumeInfo.imageLinks.thumbnail"
        style="flex-basis: 125px"
      ></v-img>
    </v-row>
    <v-divider dark></v-divider>
    <v-card-actions class="pa-4">
      Rate this album
      <v-spacer></v-spacer>
      <span class="grey--text text--lighten-2 caption mr-2">
        <!-- ({{ rating }}) -->
      </span>
      <v-rating
        v-model="rating"
        background-color="white"
        color="yellow accent-4"
        dense
        half-increments
        hover
        size="18"
      ></v-rating>
    </v-card-actions>
  </v-card>
    
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
        loopData: [],
        titles: [],
        searchField: "",
        src: "",
      }
    },
    methods: {

      getImage: function(path) {
        return require(path)
      },

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
      this.loopData = [];
      for (var j = 0; j < this.data.items.length; j++) {
        var newItem = this.data.items[j];
        this.loopData.push(newItem);
        console.log(newItem.volumeInfo.imageLinks.thumbnail);
      }
      console.log(this.loopData);
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




