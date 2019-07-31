<template>
  <div id="app">
    <Header/>
    <Hero/>
    <Body/>
    <Footer/>
  </div>
</template>

<script>
// dependencies
import 'bootstrap/dist/css/bootstrap.css'

//components
import Header from './components/Header.vue'
import Hero from './components/Hero.vue'
import Body from './components/Body.vue'
import Footer from './components/Footer.vue'

let WebFont = require('webfontloader');

WebFont.load({
    google: {
      families: ['Open Sans', 'Cousine']
    }
  });

export default {
  name: 'app',
  components: {
    Header,
    Hero,
    Body,
    Footer
  }
}
</script>

<style>
body{overflow-x:hidden;}
ul{padding:0;}
li{list-style:none;padding:0;}
textarea:focus, input:focus{outline: none;}
button{ border: none;
    margin: 0;
    padding: 0;
    width: auto;
    overflow: visible;
    background: transparent;}
#app {
  font-family: 'Cousine', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
h1{
  font-family:'Open Sans';
  font-size:55px;
}
h2{
  font-size:25px;
}
h3{
  font-size:20px;
}
.text-underline{
  border-bottom:tomato;
  border-width:5px;
}
    .cta{
        position:absolute;
        color:white;
        padding:30px 50px 30px 50px;
        outline:0;
        left:50%;
        transform:translateX(-50%);
        bottom:-60%;
        line-height:5px;
        white-space:nowrap;
        font-size:25px;
        letter-spacing:0;
        font-weight: 500;
        border-color: tomato;
        border-style: none none solid;
        border-width: 10px 0px 10px;
        padding: 0px 0px 5px;
        transition:0.2s ease-out;
    }
    .cta:hover{
         border-width: 0px 0px 0px;
    }
</style>
