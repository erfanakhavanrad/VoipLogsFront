<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import SockJS from "sockjs-client";
import Stomp from "webstomp-client";

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  mounted(){
    const socket = SockJS('http://localhost:8080/connect')
    this.stompClient = Stomp.over(socket)
    
    // stompClient.connect({},Frame => 
    // console.log(Frame))
          this.stompClient.connect(
        {},
        frame => {
        //  this.connected = true;
          console.log(frame);
          this.stompClient.subscribe("/topic/messages", tick => {
          console.log(tick);
          console.log(JSON.parse(tick.body).content);
          });
        },
        error => {
          console.log(error);
         // this.connected = false;
        }
      )
    }

  }
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
