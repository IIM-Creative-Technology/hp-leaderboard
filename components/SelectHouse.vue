<template>
    <main class="selectHouseMain">
        <div>
            <img src="../static/assets/snake.png" class="noOpacity" @click="$emit('select', 1)" :class="{opacity : imageHover !== 1 && imageHover !== null}" @mouseover="imageHover = 1" @mouseleave="imageHover = null" alt="Snake">
            <img src="../static/assets/eagle.png" class="noOpacity" @click="$emit('select', 2)" alt="Eagle" :class="{opacity : imageHover !== 2 && imageHover !== null}" @mouseover="imageHover = 2" @mouseleave="imageHover = null">
            <img src="../static/assets/badger.png" class="noOpacity" @click="$emit('select', 3)" alt="Badger" :class="{opacity : imageHover !== 3 && imageHover !== null}" @mouseover="imageHover = 3" @mouseleave="imageHover = null">
            <img src="../static/assets/lion.png" class="noOpacity" @click="$emit('select', 4)" alt="Lion" :class="{opacity : imageHover !== 4 && imageHover !== null}" @mouseover="imageHover = 4" @mouseleave="imageHover = null">
        </div>
        
    </main>
</template>

<script>
export default {
    props: ['houseId'],
    data() {
        return {
            imageHover : null,
        }
    },
}
</script>

<style>
    .selectHouseMain {
        display: flex;
        height: 100vh;
        margin: auto;
        align-items: center;
        background: var(--color-light);
    }

    .selectHouseMain div {
        width: 90vw;
        margin: auto;
        display: flex;
        justify-content: space-around;
    }

    .selectHouseMain img {
        width: 20vw;
        border-radius: var(--radius);
        cursor: pointer;
    }

    .opacity {
        opacity: 15% !important;
        transition: 0.6s;
    }

    .noOpacity {
        opacity: 100%;
        transition: 0.6s;
    }
</style>