<template>
    <div :class="['user-box', position]">
        <img :src="user.picture.large" alt="User Picture" />
        <h3>{{ user.name.first }} {{ user.name.last }}</h3>
        <div class="color-box" :style="{ backgroundColor: bgColor }"></div>
        <textarea v-model="message" placeholder="Escribe tu mensaje..."></textarea>
        <button @click="sendMessage">Enviar</button>
    </div>
</template>

<script>
export default {
    props: {
        user: Object,
        bgColor: String,
        position: String
    },
    data() {
        return {
            message: ''
        };
    },
    methods: {
        sendMessage() {
            if (this.message.trim()) {
                this.$emit('send-message', {
                    user: this.user,
                    text: this.message,
                    color: this.bgColor
                });
                this.message = '';
            }
        }
    }
};
</script>

<style scoped>
.user-box {
    width: 25%;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 10px;
}

.left {
    float: left;
}

.right {
    float: right;
}

textarea {
    width: 100%;
    height: 80px;
    margin-top: 10px;
}

button {
    margin-top: 10px;
}

.color-box {
    width: 130px;
    height: 30px;
    margin: 10px 0;
    border: 1px solid #ccc;
}
</style>