<template>
<transition name="slide" >
  <div v-if="show" class="chatmessage">
    <div class="chatmessage-user">{{ chat.tags.username }}</div>
    <div>{{ chat.message }}</div>
  </div>
</transition>
</template>

<script>
export default {
  name: 'ChatMessage',
  props: {
    chat: {
      tags: Object,
      message: String
      },
  },
  data() {
    return {
      show: false
    }
  },
  mounted() {
    setTimeout(() => {
      this.show = true;
    }, 1);
  },
  beforeUnmount() {
    this.show = false;
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.chatmessage {
  display: grid;
  grid-template-rows: 1fr auto;
  width: 400px;
  text-align: start;
  margin: 0.5rem;
  background: #000000CC;
  color: #cc3399;
  padding: 1rem;
} 

.chatmessage-user {
  margin: 0;
  font-weight: 600;
}

.slide-enter-active,
.slide-leave-active {
  transition: all 1s ease;
}

.slide-enter-from,
.slide-leave-to {
  transform: translate(100%);
}

</style>
