<template>
    <section class="podiumSection">
     <div>
        <img id="first" src="../static/assets/lion.png" alt="Lion">
        <img id="second" src="../static/assets/snake.png" alt="Snake">
        <img id="third" src="../static/assets/badger.png" alt="Badger">
     </div> 
    </section>
</template>

<script>
export default {
    
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

    .podiumSection #first {
        width: 100%;
        position: relative;
        z-index: 100;
    }

    .podiumSection #second {
        width: 80%;
        position: absolute;
        top: 35%;
        right: 80%;
        z-index: 10;
    }

    .podiumSection #third {
        width: 65%;
        position: absolute;
        top: 60%;
        left: 70%;
        z-index: 1;
    }
</style>