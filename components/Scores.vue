<template>
    <section class="leadSection">
      <h2>TEAMS SCORES</h2>

      <div class="scoresList">
        <p class="vicString">Gryffindor points</p>
        <p class="vicNumber">{{ gryffondorPoints }}</p>
        <div class="vicRange"><div id="gryffRange" :style="cssProps"></div></div>
      </div>

      <div class="scoresList">
        <p class="vicString">Hufflepuff points</p>
        <p class="vicNumber">{{ pouffsoufflePoints }}</p>
        <div class="vicRange"><div id="pouffRange" :style="cssProps"></div></div>
      </div>

      <div class="scoresList">
        <p class="vicString">Ravenclaw points</p>
        <p class="vicNumber">{{ serdaiglePoints }}</p>
        <div class="vicRange"><div id="serdRange" :style="cssProps"></div></div>
      </div>

      <div class="scoresList">
        <p class="vicString">Slytherin points</p>
        <p class="vicNumber">{{ serpentardPoints }}</p>
        <div class="vicRange"><div id="serpRange" :style="cssProps"></div></div>
      </div>
    </section>
</template>

<script>
export default {
    props: ["serpentardPoints","serdaiglePoints","pouffsoufflePoints","gryffondorPoints"],
    computed: {
        cssProps() {
            return {
                '--gryff-percentage': ((this.gryffondorPoints / (this.gryffondorPoints + this.pouffsoufflePoints + this.serdaiglePoints + this.serpentardPoints)) * 100) + "%",
                '--pouff-percentage': ((this.pouffsoufflePoints / (this.gryffondorPoints + this.pouffsoufflePoints + this.serdaiglePoints + this.serpentardPoints)) * 100) + "%",
                '--serp-percentage': ((this.serpentardPoints / (this.gryffondorPoints + this.pouffsoufflePoints + this.serdaiglePoints + this.serpentardPoints)) * 100) + "%",
                '--serd-percentage': ((this.serdaiglePoints / (this.gryffondorPoints + this.pouffsoufflePoints + this.serdaiglePoints + this.serpentardPoints)) * 100) + "%",
            }
        }
    },
}
</script>

<style scoped>
    .leadSection {
        width: 22%;
        height: 100%;
        background: var(--color-dark);
        border-radius: var(--radius);
    }

    .leadSection h2 {
        color: var(--color-white);
        font-size: 1.2rem;
        padding-left: 10%;
        padding-top: 10vh;
    }

    .leadSection .scoresList {
        width: 80%;
        margin: 6vh auto;
    }

    .leadSection .vicString {
        font-size: 0.7rem;
        color: var(--color-white);
    }

    .leadSection .vicNumber {
        font-size: 1.8rem;
        color: var(--color-white);
    }

    .leadSection .vicRange {
        width: 100%;
        height: 10px;
        background: #1E1828;
        border-radius: 10rem;
        transition: 1s;
    }

    .leadSection .vicRange div {
        height: 100%;
        border-radius: 10rem;
        transition: 1s;
    }

    .leadSection .vicRange #gryffRange {
        background: red;
        width: var(--gryff-percentage);
    }

    .leadSection .vicRange #pouffRange {
        background: yellow;
        width: var(--pouff-percentage);
    }

    .leadSection .vicRange #serpRange {
        background: green;
        width: var(--serp-percentage);
    }

    .leadSection .vicRange #serdRange {
        background: blue;
        width: var(--serd-percentage);
    }
</style>