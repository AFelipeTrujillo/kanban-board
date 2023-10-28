<script setup>
import { ref, defineEmits } from 'vue';

    const text = ref('')
    const emits = defineEmits(['onNewItem'])

    function hanbleSubmit(){
        if(text != ''){
            emits('onNewItem', text)
            text.value = ''
        } 
    }
</script>

<template>
    <form @submit.prevent="hanbleSubmit">
        <input type="text" v-bind="text" />
    </form>
</template>

<style scoped></style>