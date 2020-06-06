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
                @keyup.enter="getRequest"
                :persistent-hint="hint"
                :hint = "invalidISBN"
              ></v-text-field>
          </v-flex>
          <v-flex sm2>
              <v-btn v-on:click="getRequest" color="#00b9be" medium dark 
                    :loading="loading">Search
                <v-icon dark right>fas fa-search</v-icon>
            </v-btn>
          </v-flex>

         <v-tooltip left>
            <template v-slot:activator="{ on }">
              <v-btn
                v-scroll="onScroll"
                v-show="fab"
                fab
                dark
                fixed
                bottom
                right
                color="#808080"
                @click="toTop"
                v-on="on"
              >
                <v-icon>fas fa-chevron-up</v-icon>
              </v-btn>
            </template>
            <span>Scroll to top</span>
          </v-tooltip>
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
           
            <!-- Multi-result, 1/3 width card -->
            <v-card v-if="!singleResult" 
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
                      <div style="font-weight: 500; color: white; word-break: normal;" v-text = "book.volumeInfo.title" class="headline"></div>
                      <div style="font-weight: 300; color: white; word-break: normal;" v-text = "book.volumeInfo.authors"></div>
                      <div style="font-weight: 300; color: white; word-break: normal;" v-text = "book.volumeInfo.publishedDate"></div>
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
                
                <div style="font-size: 14px; white-space: pre;" v-text = "book.volumeInfo.industryIdentifiers[0].identifier + '\n' + book.volumeInfo.industryIdentifiers[1].identifier"></div>
                <v-spacer></v-spacer>

                <div style="font-size: 14px; postion:relative; padding-bottom: 0px; padding-left: 50px; word-break: normal;" v-text = "book.volumeInfo.ratingsCount" ></div>

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
            
            <!-- Single-result, full width card -->
            <v-card v-if="singleResult" 
              v-on="on"
              class="mx-auto elevation-20"
              color="#00b9be"
              dark
            >
              <v-row justify="space-between" v-if="book.show">
                <v-col cols="8">
                  <v-card-title primary-title>
                    <div>
                      <div style="font-weight: 500; color: white; word-break: normal;" v-text = "book.volumeInfo.title" class="headline"></div>
                      <div style="font-weight: 300; color: white; word-break: normal;" v-text = "book.volumeInfo.authors"></div>
                      <div style="font-weight: 300; color: white; word-break: normal;" v-text = "book.volumeInfo.publishedDate"></div>
                    </div>
                  </v-card-title>
                </v-col>
                <v-img
                  
                  contain
                  :src = "book.volumeInfo.imageLinks.thumbnail"
                  alt="No image available"
                  
                ></v-img>
              </v-row>
              <v-divider color="grey" v-if="book.show"></v-divider>
              <v-card-actions class="pa-4" v-if="book.show">
                
                <div style="font-size: 14px; white-space: pre;" v-text = "book.volumeInfo.industryIdentifiers[0].identifier + '\n' + book.volumeInfo.industryIdentifiers[1].identifier"></div>
                <v-spacer></v-spacer>

                <div style="font-size: 14px; postion:relative; padding-bottom: 0px; padding-left: 50px; word-break: normal;" v-text = "book.volumeInfo.ratingsCount" ></div>

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
          <div style="font-weight: 500; color: Black; word-break: normal;" v-text = "book.volumeInfo.title" class="headline"></div>
        </v-card-title>

        <v-card-text style="font-size: 15px; font-weight: 500">
          Description:
        
          <div style="font-size: 14px; font-weight: 300; postion:relative; word-break: normal;" v-text = "book.volumeInfo.description" ></div>       
        </v-card-text>

        <v-divider></v-divider>

        
        <v-btn tile outlined :href="book.volumeInfo.amazon" target="_blank" style="padding-left: -50px; padding-top: 10px; font-size: 15px; font-weight: 500; word-break: normal;">
            <v-icon left>fas fa-shopping-basket</v-icon> Buy on Amazon
        </v-btn>
        
          
       


        </v-card>
      
      </v-dialog>
    

    
    

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

        singleResult: false,

        fab: false,
        invalidISBN: "",
        hint: true,

        loading: false
      }
    },
    methods: {

      getImage: function(path) {
        return require(path)
      },

      getRequest: function(){

        let maxResults = "&maxResults=40";
        this.singleResult = false;

        const isbn = this.searchField.split("-").join("");
        if ((isbn.length === 10 || isbn.length === 13) && !isNaN(isbn.replace("X", "0"))) {
          this.singleResult = true;
          if (!this.isValidISBN(isbn)) {
            this.invalidISBN = "THIS IS NOT A VALID ISBN.";
            return;
          }
          maxResults = "&maxResults=1";
        }

        this.loading = true;

        const splitString = this.searchField.split(" ").join("+");
        let url = "https://www.googleapis.com/books/v1/volumes?q=" + splitString + maxResults;
        console.log(url);
        this.loopData = [];
        this.invalidISBN = "";

        fetch(url)
        .then(data =>{return data.json()})
        .then(res =>{this.data = res;
                     this.handleResponse()})
        // .catch(error=>this.data = "Nothing Found!");   
      },

      handleResponse: function() {
        console.log(this.data);
        this.loading = false;

        if (this.data.items.length == 1) {
          this.singleResult = true;
        }

        for (var j = 0; j < this.data.items.length; j++) {

          var newItem = this.data.items[j];
          try{
            newItem.volumeInfo.authors = newItem.volumeInfo.authors.toString();
          }catch{
            newItem.volumeInfo.authors = "author unknown";
          }
          //text trunctation
          if(newItem.volumeInfo.authors.length > 40){
            newItem.volumeInfo.authors = newItem.volumeInfo.authors.slice(0, 40) + '...';
            
          }
          
          if(newItem.volumeInfo.title.length > 50){
            newItem.volumeInfo.title = newItem.volumeInfo.title.slice(0,50) + '...';
          }

          newItem.volumeInfo.amazon = "https://www.amazon.com/s?k=" + newItem.volumeInfo.title.split(' ').join('+') + "&i=stripbooks&ref=nb_sb_noss_2";

          if(newItem.volumeInfo.ratingsCount){
            newItem.volumeInfo.ratingsCount = newItem.volumeInfo.ratingsCount + " Google User Reviews";
          }else{
            newItem.volumeInfo.ratingsCount = "No" + " Google User Reviews";
          }

          let isbn10 = "";
          let isbn13 = "";

          try{
            let identifier0 = newItem.volumeInfo.industryIdentifiers[0].identifier;
            let type0 = newItem.volumeInfo.industryIdentifiers[0].type;

            if (type0 == "ISBN_10") {
              isbn10 = "ISBN (10 DIGIT):\n" + identifier0;
            }
            if (type0 == "ISBN_13") {
              isbn13 = "ISBN (13 DIGIT):\n" + identifier0;
            }
          }catch{
            console.log("NO ISBN[0] PROVIDED");
          }

          try{
            let identifier1 = newItem.volumeInfo.industryIdentifiers[1].identifier;
            let type1 = newItem.volumeInfo.industryIdentifiers[1].type;

            if (type1 == "ISBN_10") {
              isbn10 = "ISBN (10 DIGIT):\n" + identifier1;
            }
            if (type1 == "ISBN_13") {
              isbn13 = "ISBN (13 DIGIT):\n" + identifier1;
            }
          }catch{
            console.log("NO ISBN[1] PROVIDED");
          }

          newItem.volumeInfo.industryIdentifiers[0].identifier = isbn10;
          newItem.volumeInfo.industryIdentifiers[1].identifier = isbn13;
          
          newItem.show = true;

          this.loopData.push(newItem);
          
        }

        // spacers are cards that wont show up, to allow centering.
        // indicate a spacer by setting book.show to false.
        if (this.singleResult) {
          let spacer = JSON.parse(JSON.stringify(this.loopData[0]));
          spacer.show = false;
          this.loopData.unshift(spacer);
          this.loopData.push(spacer);
        }


        console.log(this.loopData);
      },

      onScroll: function(e) {
      if (typeof window === 'undefined') return
      const top = window.pageYOffset ||   e.target.scrollTop || 0
      this.fab = top > 20
      },

      toTop: function() {
        this.$vuetify.goTo(0)
      },

      isValidISBN: function(number_to_test) {
        let sum = 0;
        let num = number_to_test.toString().split("-").join("");
        if (num.length !== 10 && num.length !== 13) {
          return false;
        }
        if (isNaN(num.replace("X", "0"))) {
          return false;
        }

        if (num.length === 10) {
          let x = 0;
          for (let i = num.length; i > 0; i--) {
            if (num[x] == "X") {
              sum = sum + (i * 10);
            }
            else {
              sum = sum + (i * parseInt(num[x]));
            }
            x++;
          }

          return (sum % 11 === 0);
        }

        else {
          let x = true;
          for (let i = 0; i < num.length; i++) {
            if (num[i] == "X") {
              if (x) {
                sum = sum + 10;
                x = !x;
              }
              else {
                sum = sum + 30;
                x = !x;
              }
            }
            else {
              if (x) {
                sum = sum + parseInt(num[i]);
                x = !x;
              }
              else {
                sum = sum + (3 * parseInt(num[i]));
                x = !x;
              }
            }
          }
          return (sum % 10 === 0);
        }
      },

      

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




