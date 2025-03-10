<script setup>
const props = defineProps({
    value: {
        type: String,
        required: true
    }
});

const emit = defineEmits(['send-value']);
</script>

<template>
    <button @click="emit('send-value', props.value)">{{ props.value }}</button>
</template>

<style scoped>
button {
    border: 2px solid black;
    background-color: whitesmoke;
    padding: 5px;
    color: black; 
    text-align: center;
    border-radius: 5px;
    height: 60px;
    width: 60px;
}
</style>
