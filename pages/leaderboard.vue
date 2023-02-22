<template>
    <main class="leaderboardMain">
        <div class="leaderboardSections">
            <Scores :serpentard-points="serpentardPoints" :serdaigle-points="serdaiglePoints" :pouffsouffle-points="pouffsoufflePoints" :gryffondor-points="gryffondorPoints" />
            <div class="leadRightSide">
                <Podium/>
                <div class="leadBottomRight">
                    <Bonus/>
                    <Classement/>
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


export default {
    name: "LeaderboardPage",
    data() {
        return {
            serpentardPoints: null,
            serdaiglePoints: null,
            pouffsoufflePoints: null,
            gryffondorPoints: null,
        };
    },
    mounted: async function() {
        try {
            const response = await axios.get('https://hp-api-iim.azurewebsites.net/houses');
            this.serpentardPoints = response.data[0].points;
            this.serdaiglePoints = response.data[1].points;
            this.pouffsoufflePoints = response.data[2].points;
            this.gryffondorPoints = response.data[3].points;
        } catch (error) {
            console.error(error);
        }
    },
    components: { Scores, Podium }
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