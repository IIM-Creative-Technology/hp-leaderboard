<template>
    <section class="classementSection">
        <h2>Ranking</h2>
        <div class="tab" id="tabHeader">
            <p class="row">House</p>
            <p class="row">Player</p>
            <p class="row">Game</p>
            <p class="row">Points</p>
        </div>
        <div class="tab" id="tabLine" v-for="log in logsReversed" :key="log.id">
            <p class="row">{{ log.user.house.name }}</p>
            <p class="row">{{ log.user.name }}</p>
            <p class="row">{{ log.match.game }}</p>
            <p class="row">+{{ log.points }}</p>
        </div>
    </section>
</template>

<script>
export default {
    props: ['logs'],
    computed: {
        logsReversed() {
            return this.logs?.reverse()
        }
    }
}
</script>

<style scoped>
    .classementSection {
        width: 73.7%;
        height: 100%;
        background: var(--color-dark);
        border-radius: var(--radius);
        overflow-y: auto;
    }

    /* // scrollbar style */

    ::-webkit-scrollbar, ::-webkit-scrollbar-track  {
        visibility: hidden;
        width: 5px;
    }

    ::-webkit-scrollbar-thumb {
        background-color: var(--color-gray);
        border-radius: 100vw;
    }

    ::-webkit-scrollbar-thumb:hover {
        background-color: rgb(175, 175, 175);
    }

    ::-webkit-scrollbar-thumb:active {
        background-color: rgb(150, 150, 150);
    }

    .classementSection::webkit-scrollbar {
        width: 12px;
    }

    .classementSection::-webkit-scrollbar-track {
        -webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.3); 
        border-radius: 10px;
    }

    .classementSection::-webkit-scrollbar-thumb {
        border-radius: 10px;
        -webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.5);
    }

    .classementSection h2 {
        color: var(--color-white);
        font-size: 1.2rem;
        padding: 30px 4%;
    }
    
    .classementSection .tab {
        width: 92%;
        margin: 0 auto;
        display: flex;
        justify-content: space-between;
    }

    .classementSection #tabHeader p {
        color: var(--color-gray);
        padding-bottom: 20px;
    }

    .classementSection #tabLine {
        border-top: 1px solid #8a8a8a40;
    }

    .classementSection #tabLine p {
        color: var(--color-white);
        padding: 15px 0;
    }

    .row {
        width: 25%;
        text-align: center;
    }

</style>