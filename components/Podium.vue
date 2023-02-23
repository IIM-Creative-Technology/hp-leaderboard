<template>
    <section class="podiumSection">
     <div v-if="houses && houses.length">
        <img :class="{'first': findLeaderboardIndex(1, 3), 'second': findLeaderboardIndex(1, 2), 'third': findLeaderboardIndex(1, 1), 'none': findLeaderboardIndex(1, 0) }" src="../static/assets/snake.png" alt="Snake">
        <img :class="{'first': findLeaderboardIndex(2, 3), 'second': findLeaderboardIndex(2, 2), 'third': findLeaderboardIndex(2, 1), 'none': findLeaderboardIndex(2, 0) }" src="../static/assets/lion.png" alt="Lion">
        <img :class="{'first': findLeaderboardIndex(3, 3), 'second': findLeaderboardIndex(3, 2), 'third': findLeaderboardIndex(3, 1), 'none': findLeaderboardIndex(3, 0) }" src="../static/assets/eagle.png" alt="Eagle">
        <img :class="{'first': findLeaderboardIndex(4, 3), 'second': findLeaderboardIndex(4, 2), 'third': findLeaderboardIndex(4, 1), 'none': findLeaderboardIndex(4, 0) }" src="../static/assets/badger.png" alt="Badger">
     </div> 
    </section>
</template>

<script>
import { computed } from 'vue';

export default {
    props: ['houses'],
    setup(props) {
        const leaderboard = computed(() => {
            return props.houses?.sort((a, b) => a.points - b.points).map(house => house.id)
        })

        function findLeaderboardIndex(houseId, rank) {
            return leaderboard.value.findIndex(id => id === houseId) === rank
        }

        return {
            leaderboard,
            findLeaderboardIndex
        }
    }
}
</script>

<style scoped>
    .podiumSection {
        width: 100%;
        height: 45%;
        background: var(--color-dark);
        border-radius: var(--radius);
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .podiumSection div {
        width: 27vh;
        position: relative;
        bottom: 3.5vh;
    }

    .podiumSection img {
        border-radius: 50em;
        width: 100%;
    }

    .podiumSection .first {
        width: 100%;
        position: relative;
        z-index: 100;
    }

    .podiumSection .second {
        width: 80%;
        position: absolute;
        top: 35%;
        right: 80%;
        z-index: 10;
    }

    .podiumSection .third {
        width: 65%;
        position: absolute;
        top: 60%;
        left: 70%;
        z-index: 1;
    }

    .podiumSection .none {
        display: none;
    }
</style>