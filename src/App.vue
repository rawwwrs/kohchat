<template>
  <div id="messagelist">
    <ChatMessage 
    v-for="(message, index) in messages"
    :key="message"
    :chat="message"
    :index="index"
    />
  </div>
</template>

<script>
import ChatMessage from './components/ChatMessage.vue';

const socket = require('socket.io-client')('ws://192.168.178.47:3000', {reconnectionDelayMax: 10000});

export default {
  name: 'App',
  components: {
    ChatMessage,
  },
  data() {
    return { messages: [] }
  },
  mounted(){
    socket.on("connect", () => {
      console.log("connected");
    })
    socket.on("message", (data) => {
      this.addMessage(data);
    });
  },
  unmounted(){
    socket.on("disconnect", () => {
      console.log("disconnected");
    })
  },
  methods: {
    addMessage(message) {
      console.log(message);
      this.messages = [...this.messages, message];
      if (this.messages.length > 4) {
      // TODO: work out leave transition 
        this.messages.shift();
      }
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
