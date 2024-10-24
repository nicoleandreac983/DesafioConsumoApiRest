<script setup>

</script>

<script>
import Chat from './components/Chat.vue';
import UserBox from './components/UserBox.vue';
import axios from 'axios';

export default {
  components: {
    Chat,
    UserBox
  },
  data() {
    return {
      user1: null,
      user2: null,
      user1Color: '#cce7ff',
      user2Color: '#ffffff',
      messages: []
    };
  },
  methods: {
    async fetchUsers() {
      try {
        const response1 = await axios.get('https://randomuser.me/api/');
        const response2 = await axios.get('https://randomuser.me/api/');
        this.user1 = response1.data.results[0];
        this.user2 = response2.data.results[0];
      } catch (error) {
        console.error('Error fetching users:', error);
      }
    },
    addMessage({ user, text, color }) {
      this.messages.push({
        name: `${user.name.first} ${user.name.last}`,
        text,
        color,
        position: user === this.user1 ? 'left' : 'right'
      });
    }
  },
  created() {
    this.fetchUsers();
  }
};
</script>

<template>
  <div class="app-container">
    <UserBox v-if="user1" :user="user1" :bgColor="user1Color" @send-message="addMessage" position="left" />

    <Chat :messages="messages" />

    <UserBox v-if="user2" :user="user2" :bgColor="user2Color" @send-message="addMessage" position="right" />
  </div>
</template>

<style scoped>
.app-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 100vh;
  padding: 20px;
}
</style>