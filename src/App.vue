<template>
  <div  id="app">
    <img alt="Vue logo" src="https://tarazgroup.com/template/pr_tarazgroup/img/logo.png" @click="connect2()">
    <notifications style="direction:rtl" ></notifications>
    <HelloWorld msg="به سامانه ویپ تراز خوش آمدید"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Notifications from '@voerro/vue-notifications'
import notify from '@voerro/vue-notifications/src/interface';

export default {
  name: 'App',
  components: {
    HelloWorld,
    Notifications
  },
 data() {
    return {
      test: null
    }
  },
  methods :{
    connect(){
   const socket = new WebSocket('ws://localhost:8080/my-websocket-endpoint');
   socket.onopen = function() {
 //   alert('WebSocket connection opened. Ready to send messages.');
 
  socket.send('Hello, from WebSocket client!');
};
 
  },
  connect2(){
    // alert('a')
 const socket = new WebSocket('ws://localhost:8080/my-websocket-endpoint');
socket.onmessage = function(message) {
 //alert('Message received from server: ' + message.data);
//  const self = this

  
  if(message.data == 'null'){
    //console.log('MESSAGE WAS NULL'+ message.data);
  } else {
    this.test = message.data
 
  // let number = 1
  
  //  notify(message.data)

notify({
    text: message.data,
    theme: 'blue',
    hideafter: 500
});

   return;
  //  number = number +1
// console.log(number);

  
  }

};

  },    
     },
mounted: function () {
  window.setInterval(() => {
    this.connect2()
  }, 1000)
},
  watch:{
     test:{
     handler(newVal) {
      if (newVal.includes('null')) {
        notify('call ended')
      }}

  }
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
