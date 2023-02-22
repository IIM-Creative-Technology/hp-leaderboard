<template>
    <div v-if="houses && houses.length">
        {{ houses }}
        {{ matches }}
    </div>
</template>

<script setup lang="ts">
import axios from 'axios'
import { onMounted, ref } from 'vue';
import { io } from "socket.io-client";

const houses = ref()
const matches = ref()

onMounted(async () => {
    const socket = io('http://localhost:8080');

    socket.on('houses', async function () {
        houses.value = await axios.get('https://hp-api-iim.azurewebsites.net/houses').then(data => data.data)
    });

    socket.on('matches', async function () {
        matches.value = await axios.get('https://hp-api-iim.azurewebsites.net/matches').then(data => data.data)
    });

    houses.value = await axios.get('https://hp-api-iim.azurewebsites.net/houses').then(data => data.data)
    matches.value = await axios.get('http://localhost:8080/matches').then(data => data.data)
})

</script>