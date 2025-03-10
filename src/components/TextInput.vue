<script setup>
    import {ref} from 'vue'
    const valeur = ref("")
</script>

<template>
    <div>
        <input type="text" name="toto" id="" v-model="valeur">
        <span>{{ valeur }}</span>
    </div>

</template>