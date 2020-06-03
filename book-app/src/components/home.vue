<template lang="html">

  


  <div id="home">

    
      <div id="heading">
            <img style="margin-top: -50px" class="image" width="300" height="300" src="../assets/bookLogo.png"> 
            <h1> Book Looker </h1>
            <h2>Search by ISBN, Author or Title</h2>
    </div>

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
  
  <v-container fluid grid-list-md>
          <v-layout row wrap>
            <v-flex
              xs12
              md6
              lg4
             v-for="(book, key) in loopData" v-bind:key="key"
            >

  <!-- <div class="list-group-item " style="margin-left: 1vw; margin-right: 1vw; margin-bottom: 1vh; " v-for="(book, key) in loopData" v-bind:key="key"> -->

    <!-- <v-list-item-title
        style="word-break: normal; padding-top: 5px; display: inline-block; font-size: 18px; max-width:45vw"
        class=" text-truncate"
        text-truncate
        v-text = "book"
    > </v-list-item-title> -->

 <v-dialog
      v-model="dialog"
      width="900"
      height="600"
    >
      <template  v-slot:activator="{ on }">
        <div style="padding-bottom: 50px;">
          <v-card
              
              v-on="on"
              class="mx-auto elevation-20"
              color="#00b9be"
              dark
              style="max-width:360px; max-height:350px; min-width:360px; min-height:350px"
            >
              <v-row justify="space-between">
                <v-col cols="8">
                  <v-card-title primary-title>
                    <div>
                      <div style="font-weight: 500; color: white" v-text = "book.volumeInfo.title" class="headline"></div>
                      <div style="font-weight: 300; color: white" v-text = "book.volumeInfo.authors"></div>
                      <div style="font-weight: 300; color: white" v-text = "book.volumeInfo.publishedDate"></div>
                    </div>
                  </v-card-title>
                </v-col>
                <v-img
                  
                  contain
                  :src = "book.volumeInfo.imageLinks.thumbnail"
                  alt="No image available"
                  
                ></v-img>
              </v-row>
              <v-divider color="grey"></v-divider>
              <v-card-actions class="pa-4">
                
                <div style="font-size: 14px;" v-text = "book.volumeInfo.industryIdentifiers[1].identifier"></div>
                <v-spacer></v-spacer>

                <div style="font-size: 14px; postion:relative; padding-bottom: 0px; padding-left: 50px" v-text = "book.volumeInfo.ratingsCount" ></div>

                <v-rating
                  v-model="book.volumeInfo.averageRating"
                  readonly="readonly"
                  background-color="white"
                  color="yellow accent-4"
                  dense
                  half-increments
                  
                  size="18"
                ></v-rating>
              </v-card-actions>
            </v-card>
            </div>
      </template>

      <v-card>
        <v-card-title
          class="headline"
          primary-title
        >
          <div style="font-weight: 500; color: Black" v-text = "book.volumeInfo.title" class="headline"></div>
        </v-card-title>

        <v-card-text>
          Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
        </v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="#00b9be"
            text
            @click="dialog = false"
          >
            Close
          </v-btn>
        </v-card-actions>
      </v-card>
      
    </v-dialog>
    

    
    
  <!-- </div> -->

            </v-flex>
          </v-layout>
        </v-container>

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
        rating: 5,
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
          try{
            newItem.volumeInfo.authors = newItem.volumeInfo.authors.toString();
          }catch{
            console.log("caught");
          }

          // try{
          //   if(newItem.volumeInfo.imageLinks.thumbnail = null)
          //   console.log(image);
          // }catch{
          //   newItem.volumeInfo.imageLinks.thumbnail = "https://comnplayscience.eu/app/images/notfound.png";
          // }

          newItem.volumeInfo.ratingsCount = newItem.volumeInfo.ratingsCount + " Google User Reviews";
          try{
            newItem.volumeInfo.industryIdentifiers[0].identifier = "ISBN: " + newItem.volumeInfo.industryIdentifiers[0].identifier;
          }catch{
            console.log("caught");
          }
          
          this.loopData.push(newItem);
  
          
        }


        console.log(this.loopData);
    }

      

    },
    computed: {

    }
}


</script>


<style scoped>

h1{
  margin-top: -80px;
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






</style>>




