<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <button @click="connect()"></button>
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
// import SockJS from "sockjs-client";
//import Stomp from "webstomp-client";


export default {
  name: 'App',
  components: {
    HelloWorld
  },

  methods :{
        send() {
    //  console.log("Send message:" + this.send_message);
      if (this.stompClient && this.stompClient.connected) {
        const msg = 'test'
        alert(JSON.stringify(msg));
        this.stompClient.send("/ws/start", JSON.stringify(msg), {});
      }
    },
    connect(){
        const socket = new WebSocket('ws://localhost:8080/my-websocket-endpoint');
socket.onopen = function() {
  alert('WebSocket connection opened. Ready to send messages.');
 
  socket.send('Hello, from WebSocket client!');
};
 
socket.onmessage = function(message) {
  console.log('Message received from server: ' + message.data);
};
    }
  },
  mounted(){
           const socket = new WebSocket('ws://localhost:8080/my-websocket-endpoint');
socket.onopen = function() {
  alert('WebSocket connection opened. Ready to send messages.');
 
  socket.send('Hello, from WebSocket client!');
};
 
socket.onmessage = function(message) {
 alert('Message received from server: ' + message.data);
};
    
       
    //  console.log("Send message:" + this.send_message);
//      const socket = SockJS('http://localhost:8080/my-websocket-endpoint')
//     //  const socket = new WebSocket('ws://http://localhost:8080/test')
//     // const socket = new WebSocket('ws://' + 'http://localhost:8080' + '/test')
// // var socket = new WebSocket('ws://localhost:8080/my-websocket-endpoint');

    
// // Add an event listener for when a connection is open
// socket.onopen = function() {
//   alert('WebSocket connection opened. Ready to send messages.');
 
//   // Send a message to the server
//   socket.send('Hello, from WebSocket client!');
// };
 
// // Add an event listener for when a message is received from the server
// socket.onmessage = function(message) {
//   console.log('Message received from server: ' + message);
// };
    // this.stompClient = Stomp.over(socket)
    // // stompClient.connect({},Frame => 
    // // console.log(Frame))
    //       this.stompClient.connect(
    //     {},
    //     frame => {
    //     //  this.connected = true;
    //       console.log(frame.body.content);
    //       console.log(document.URL);
    //       this.stompClient.subscribe("/messages", tick => {
    //       alert("tickkk" + tick);
    //       console.log(JSON.parse(tick.body).content);
    //       });
    //     },
    //     // error => {
    //     //   console.log(error);
    //     //  // this.connected = false;
    //     // }
    //   )
    //     // const msg = 'test'
    //     // alert(JSON.stringify(msg));
    //     // this.stompClient.send("/ws/send", {});
    
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
