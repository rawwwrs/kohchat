<template>
  <div class="chatmessage">
    <div class="chatmessage-user">{{chat.tags.username}}</div>
    <div>{{ chat.message }}</div>
  </div>
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
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.chatmessage {
  display: flex;
  text-align: start;
  margin: 0.5rem;
  background: pink;
  padding: 1rem;
  max-width: 400px;
}

.chatmessage-user {
  margin: 0 1rem;

}
</style>
