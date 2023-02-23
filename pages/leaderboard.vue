<template>
    <main class="leaderboardMain">
        <div class="leaderboardSections">
            <Scores :serpentard-points="serpentardPoints" :serdaigle-points="serdaiglePoints" :pouffsouffle-points="pouffsoufflePoints" :gryffondor-points="gryffondorPoints" />
            <div class="leadRightSide">
                <Podium :houses="houses"/>
                <div class="leadBottomRight">
                    <Bonus/>
                    <Classement :logs="logs"/>
                </div>
            </div>
        </div>
    </main>

</template>

<script>
import Scores from '../components/Scores.vue';
import Podium from '../components/Podium.vue';
import Bonus from '../components/Bonus.vue';
import Classement from '../components/Classement.vue';
import axios from 'axios';
import { computed, ref, onMounted } from 'vue';
import { io } from "socket.io-client";

export default {
    name: "LeaderboardPage",
    components: { Scores, Podium },
    setup() {
        const houses = ref()
        const logs = ref()

        const serpentardPoints = computed(() => houses.value?.find(house => house.id === 1).points)
        const gryffondorPoints = computed(() => houses.value?.find(house => house.id === 2).points)
        const serdaiglePoints = computed(() => houses.value?.find(house => house.id === 3).points)
        const pouffsoufflePoints = computed(() => houses.value?.find(house => house.id === 4).points)

        onMounted(async () => {
            const socket = io('https://hp-api-iim.azurewebsites.net');

            socket.on('houses', async function () {
                houses.value = await axios.get('https://hp-api-iim.azurewebsites.net/houses').then(data => data.data)
            });

            socket.on('matches', async function () {
                logs.value = await axios.get('https://hp-api-iim.azurewebsites.net/match-logs').then(data => data.data)
            });

            houses.value = await axios.get('https://hp-api-iim.azurewebsites.net/houses').then(data => {
                return data.data
            })
            logs.value = await axios.get('https://hp-api-iim.azurewebsites.net/match-logs').then(data => data.data)
        })

        return {
            houses,
            logs,
            serpentardPoints,
            gryffondorPoints,
            serdaiglePoints,
            pouffsoufflePoints
        }
    }
}
</script>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Poppins&display=swap');

    :root {
    --color-dark: #111212;
    --color-light: #242424;
    --color-gray: #8A8A8A;
    --color-white: white;
    --radius: 30px;
    --shadow-normal: 0 1px 3px 0 rgba(0, 0, 0, 0.1),
        0 1px 2px 0 rgba(0, 0, 0, 0.06);
    --shadow-medium: 0 4px 6px -1px rgba(0, 0, 0, 0.1),
        0 2px 4px -1px rgba(0, 0, 0, 0.06);
    --shadow-large: 0 10px 15px -3px rgba(0, 0, 0, 0.1),
        0 4px 6px -2px rgba(0, 0, 0, 0.05);
    }

    *,
    *::before,
    *::after {
        padding: 0;
        margin: 0;
    }

    .leaderboardMain {
        width: 100vw;
        height: 100vh;
        background: var(--color-light);
        font-family: 'Poppins', sans-serif;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .leaderboardSections {
        width: 97vw;
        height: 96vh;
        display:flex;
        justify-content: space-between;
    }

    .leaderboardSections .leadRightSide {
        width: 77%;
        height: 100%;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
    }

    .leaderboardSections .leadBottomRight {
        width: 100%;
        height: 53%;
        display: flex;
        justify-content: space-between;
    }
</style>