<template>
  <div id="app">
    <img id="logo" alt="Ubiqum BookStore logo" src="./assets/books.png">
    <h1>Ubiqum BookStore</h1>
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <BookComponent v-for="item in allBooks" :book="item"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import BookComponent from './components/BookComponent.vue'

export default {
  name: 'app',
  data(){
    return{
      test: 'this is a test string',
      allBooks: [
        {
          title: 'title 1',
          description: 'description 1',
          url: 'url 1'
        },
        {
          title: 'title 2',
          description: 'description 2',
          url: 'url 2'
        }]
    }
  },
  components: {
    HelloWorld,
    BookComponent
  },
  created()
  {
    console.log( 'created...' );
    this.parseJSON();
  },
  methods: {
      fetchJSON( url, init ) 
      {
        return fetch( url, init ).then( response =>
        {
            console.log( 'response ' + response );
            if( response.ok ){ return response.json(); }
            throw new Error( response.statusText );
        });
      },

    // parse json
    parseJSON()
    {
        console.log( 'parse json' );
        const url = "https://api.myjson.com/bins/zyv02";
        console.log( '=== GET DATA ===>' + url );
        this.fetchJSON( url , { method: 'GET' }).then( result => {
              console.log( 'result ' + JSON.stringify( result ) );
              this.allBooks = result.books;
              console.log( 'result ' + result.books );

              this.allBooks.forEach( item => {
                console.log( 'item ' + item.title );
              });

          });
          

    },
 
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#logo{
  width: 128px;
}
</style>
