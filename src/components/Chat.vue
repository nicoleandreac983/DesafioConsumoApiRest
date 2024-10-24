<template>
    <div class="chat-box">
        <div v-for="(message, index) in messages" :key="index" :class="['chat-message', message.position]"
            :style="{ backgroundColor: message.color }">
            <strong>{{ message.name }}</strong>
            <p>{{ message.text }}</p>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        messages: Array
    }
};
</script>

<style scoped>
.chat-box {
    width: 50%;
    height: 80vh;
    border: 1px solid #ccc;
    overflow-y: auto;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    background-color: hsl(33, 55%, 90%);
}

.chat-message {
    margin: 10px;
    padding: 10px;
    border-radius: 20px;
    max-width: 80%;
    text-transform: capitalize;
}

.left {
    align-self: flex-start;
}

.right {
    align-self: flex-end;
}
</style>