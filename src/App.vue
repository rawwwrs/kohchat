<template>
  <div id="messagelist">
    <ChatMessage 
    v-for="(message, index) in messages"
    :chat="message"
    :index="index"
    :key="message"
    />
  </div>
</template>

<script>
import ChatMessage from './components/ChatMessage.vue';

const socket = require('socket.io-client')('ws://localhost:3000', {reconnectionDelayMax: 10000});

export default {
  name: 'App',
  components: {
    ChatMessage,
  },
  mounted(){
    socket.on("connect", () => {
      console.log("connected")
    })
    socket.on("message", (data) => {
      console.log(data);
      this.addMessage(data);
    });
  },
  data() {
    return {messages: []}
  },
  methods: {
    addMessage(message) {
      this.messages = [...this.messages, message]
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#messagelist {
  display: flex;
  flex-direction: column;
  position: absolute;
  bottom: 0;
}
</style>
