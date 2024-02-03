<script setup>
import { ref, watch } from 'vue';

const todoId = ref(1);
const todoData = ref(null);

async function fetchData() {
    todoData.value = null;
    const res = await fetch(
        `https://jsonplaceholder.typicode.com/todos/${todoId.value}`
    )
    console.log(`New Count is: ${todoId.value}`)
    todoData.value = await res.json();
}

fetchData();

watch(todoId, fetchData);

</script>

<template>
    <h1>Hello</h1>
    <p>Todo id: {{ todoId }}</p>
    <button class="btn btn-dark" @click="todoId++" :disabled="!todoData">Fetch Next Todo</button>
    <p v-if="!todoData">Loading</p>
    <pre v-else>{{ todoData }}</pre>
</template>

<style scoped>
    .test {
        color: red;
    }
</style>