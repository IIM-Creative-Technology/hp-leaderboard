<template>

  <main class="signUpMain">
    <div class="signUpBlock">
      <svg fill="white" @click="$emit('select', null)" version="1.1" id="Capa_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" 
        width="50px" height="50px" viewBox="0 0 299.021 299.021"
        xml:space="preserve">
        <g>
          <g>
            <path d="M292.866,254.432c-2.288,0-4.443-1.285-5.5-3.399c-0.354-0.684-28.541-52.949-146.169-54.727v51.977
              c0,2.342-1.333,4.48-3.432,5.513c-2.096,1.033-4.594,0.793-6.461-0.63L2.417,154.392C0.898,153.227,0,151.425,0,149.516
              c0-1.919,0.898-3.72,2.417-4.888l128.893-98.77c1.87-1.426,4.365-1.667,6.461-0.639c2.099,1.026,3.432,3.173,3.432,5.509v54.776
              c3.111-0.198,7.164-0.37,11.947-0.37c43.861,0,145.871,13.952,145.871,143.136c0,2.858-1.964,5.344-4.75,5.993
              C293.802,254.384,293.34,254.432,292.866,254.432z"/>
          </g>
        </g>
      </svg>
      <img v-if="houseId === 1" src="../static/assets/snake.png" alt="snake">
      <img v-if="houseId === 2" src="../static/assets/lion.png" alt="Lion">
      <img v-if="houseId === 3" src="../static/assets/eagle.png" alt="eagle">
      <img v-if="houseId === 4" src="../static/assets/badger.png" alt="Badger">
      <div class="signUpForm">
        <input type="text" placeholder="Nickname" v-model="name">
        <input type="password" placeholder="Password" v-model="password">
        <button @click="register()">Sign Up</button>
      </div>
    </div>
  </main>

</template>

<script>
import axios from 'axios'
export default {
  props: ['houseId'],
  data() {
    return {
      name: null,
      password: null,
    }
  },

  methods: {
    async register() {
      const data = {
        name: this.name,
        password: this.password,
        houseId: this.houseId,
      }
      // if(!this.name) {  this.error = "name"; return }
      axios
        .post('https://hp-api-iim.azurewebsites.net/auth/register', data)
        .then((res) => {
          const userData = res.data
          this.$toasted.show('You have successfully signed up', {
            position: 'top-center',
            duration: 5000,
            type: 'success',
          })
          this.$router.push('/leaderboard')
        })
    },
  },
}
</script>


<style>

.signUpMain {
  display: flex;
  height: 100vh;
  margin: auto;
  align-items: center;
  background: var(--color-light);
}

.signUpMain .signUpBlock {
  width: 60vw;
  height: 250px;
  margin: auto;
  background: var(--color-dark);
  display: flex;
  justify-content: space-between;
  padding: 10vh 5vw;
  position: relative;
  border-radius: var(--radius);
}

.signUpMain .signUpBlock svg {
  position: absolute;
  top: 1vh;
  left: 5vw;
  cursor: pointer;
}

.signUpMain .signUpBlock svg:hover {
  fill: antiquewhite;
}

.signUpMain .signUpBlock img {
  border-radius: var(--radius);
}

.signUpMain .signUpBlock .signUpForm {
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 50%;
  height: 100%;
}

.signUpMain .signUpBlock input {
  height: 7vh;
  margin-bottom: 5vh;
  border-radius: var(--radius);
  border: none;
  background: #f1f5f9;
  padding-left: 2rem;
}

.signUpMain .signUpBlock button {
  width: 50%;
  margin: auto;
  border-radius: var(--radius);
  height: 7vh;
  cursor: pointer;
}

@media only screen and (max-width: 900px) {
  .signUpMain {
    min-height: 100vh;
  }

  .signUpMain .signUpBlock img {
    width: 100%;
    margin: 10vh auto;
  }

  .signUpMain .signUpBlock {
    flex-direction: column;
    background: none;
    margin: 0 auto;
    height: inherit;
    padding: 0;
  }

  .signUpMain {
    align-items: none;
  }

  .signUpMain .signUpBlock .signUpForm {
    margin: 0 auto;
    width: 100%;
    font-size: 0.8rem;
  }

  .signUpMain .signUpBlock button {
    margin-bottom: 50px;
  }

}
</style>