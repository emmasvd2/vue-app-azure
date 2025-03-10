<script setup>
import { computed } from 'vue';

const props = defineProps({
    leftOperator: {
        type: [Number, String],
        default: ""
    },
    rightOperator: {
        type: [Number, String],
        default: ""
    },
    operation: {
        type: String,
        default: ""
    },
    result: {
        type: [Number, String],
        default: ""
    }
});

const expression = computed(() => {
    return `${props.leftOperator} ${props.operation} ${props.rightOperator}`;
});
</script>

<template>
    <div class="haut">{{ expression }}</div>
    <div class="haut">{{ result }}</div>
</template>

<style scoped>
.haut {
    border: 2px solid black;
    background-color: whitesmoke;
    padding: 5px;
    color: black; 
    text-align: center;
}
</style>
