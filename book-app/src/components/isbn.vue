<template lang="html">

  <div id="home">

    
    <div id="heading">
      <div style="margin-top: 50px">
        <v-icon x-large color="#00b9be">fas fa-barcode</v-icon>
        <br>
        <span style="color: #436d6e; font-size:60%">1-5688-1111-X</span>
      </div>
      <h1> ISBN Generator </h1>
      <h2>Generate new random 10 digit ISBN</h2>
    </div>

    <div class="description">ISBN's (International Standard Book Numbers) are identifiers for books. 
      Given the correct sequence of digits, one book can be identified out of millions of others thanks 
      to this ISBN. But when is an ISBN not just a random slurry of digits? 
      <br><br>
      To verify an ISBN, you obtain the sum of 10 times the first digit, 9 times the second digit, 8 
      times the third digit... all the way till you add 1 times the last digit. If the sum leaves no 
      remainder when divided by 11 the code is a valid ISBN. If the last digit need be 10, it is 
      represented by an X
      <br><br>
      Here you can generate freshly randomized ISBN's that will all satisfy this verification.
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
            <v-tooltip right>
              <template v-slot:activator="{ on }">
                <v-btn icon color="#00b9be" v-on="on" v-on:click="copyToClip(code)">
                  <v-icon>fas fa-copy</v-icon>
                </v-btn>
              </template>
              <span>copy</span>
            </v-tooltip>
          </v-flex>
        </v-layout>
      </div>
    </div>

    <div style="margin-top:100px;">
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
        codes: [],
      }
    },
    methods: {

      generateISBN: function() {
        const newRandom = all[Math.floor(Math.random()*all.length)];
        this.codes.push(newRandom);

        return;
      },

      copyToClip: function(thing) {
        try {
          navigator.clipboard.writeText(thing);
        } catch (err) {
          console.error('Failed to copy: ', err);
        }

        return;
      },

    },
    computed: {}
}

// bunch o random ibsns
const all= ['0-1299-9170-8', '0-9384-5626-1',
            '0-1476-8627-X', '0-9212-6273-6',
            '0-5810-5604-3', '0-3145-6548-5',
            '0-3209-2070-4', '0-8154-6370-7',
            '0-2609-8846-4', '0-5157-6704-2',
            '0-9424-0471-8', '0-4044-9903-1',
            '0-2296-4229-2', '0-4360-8085-0',
            '0-7219-0624-9', '0-3774-1815-3',
            '0-6794-2079-7', '0-2263-4214-X',
            '0-9896-1183-3', '0-8488-3097-0',
            '0-6492-7894-1', '0-6828-5629-0',
            '0-8595-6305-7', '0-1761-7277-7',
            '0-8153-9997-9', '0-4621-4893-9',
            '0-9785-0608-1', '0-7498-4389-6',
            '0-2807-7184-3', '0-9753-5284-9',
            '0-7412-0064-3', '0-8822-1483-7',
            '0-8244-4147-8', '0-1272-3808-5',
            '0-2180-7017-9', '0-9344-3683-5',
            '0-8212-7640-9', '0-8832-2368-6',
            '0-6549-3382-0', '0-6549-1185-1',
            '0-3548-5287-6', '0-9747-0438-5',
            '0-3775-0166-2', '0-2696-6079-8',
            '0-5075-0900-5', '0-6653-2588-6',
            '0-8539-9315-7', '0-4264-1766-6',
            '0-7650-9283-2', '0-5652-2333-X',
            '0-1997-9753-6', '0-7766-5140-4',
            '0-1476-0797-3', '0-9195-5729-5',
            '0-4771-0852-0', '0-6415-2248-7',
            '0-7813-7648-3', '0-9895-9298-7',
            '0-6693-6100-3', '0-6564-9423-9',
            '0-6330-4128-9', '0-2902-2911-1',
            '0-1889-0254-6', '0-5916-0337-3', 
            '0-2720-0993-8', '0-1405-6088-2', 
            '0-5720-8265-7', '0-8827-6711-9',
            '0-9250-3197-6', '0-4261-5298-0',
            '0-2123-0964-1', '0-1830-8615-5',
            '0-6038-4411-1', '0-9348-6658-9',
            '0-1460-5256-0', '0-6646-5677-3',
            '0-1137-2045-9', '0-4883-3646-5',
            '0-9874-6506-6', '0-4697-9334-1',
            '0-6726-9090-X', '0-3366-8216-6',
            '0-2760-8573-6', '0-6341-7444-4', 
            '0-1073-4165-4', '0-6034-4323-0', 
            '0-5858-8633-4', '0-5041-5203-3', 
            '0-7109-8187-2', '0-3897-9104-0', 
            '0-7755-3842-6', '0-6065-5198-0', 
            '0-5756-0995-8', '0-2637-3050-6', 
            '0-5822-1460-2', '0-9881-7168-6', 
            '0-5871-4614-1', '0-1162-9019-6', 
            '0-6858-8337-X', '0-4350-0986-9'];

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

.description{
  text-align: center;
  margin-left: 10%;
  margin-right: 10%;
  margin-top: 2%;
  overflow-wrap: break-word;
}






</style>>




