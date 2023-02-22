<template>
    <!-- <div style="background-image:../static/assets/hp.jpg ;">
        <form @submit="register()" enctype="multipart/form-data" method="post">
          <div class="fields">
            <label for="nickname"><strong>Pseudo</strong></label>
            <input type="text" name="nickname" v-model="nickname" />

            <label for="password"><strong>Password</strong></label>
            <input type="password" name="password" v-model="password" />
            <span class="forgot">
              Use Uppercase, Lowercase and Numeric characters*
            </span>
          </div>

          <div class="btn">
            <button type="button" @click="register()">
              Sign Up
            </button>
          </div>
        </form>
    </div> -->

        <!-- <form @submit="register()" enctype="multipart/form-data" method="post" name="signin" class="form">
          <div class="input-control">
            <label for="name" class="input-label" hidden>Nickname</label>
            <input type="text" id="nickname" v-model="name" :class="{error : error === 'name'}" class="input-field" placeholder="Nickname">
          </div>
          <div class="input-control">
            <label for="password" class="input-label" hidden>Password</label>
            <input type="password" v-model="password" id="password" class="input-field" placeholder="Password">
          </div>
          <div class="input-control">
            <div class="select" :class="{houseSelected : houseId === 1, houseUnselected : houseId !== null && houseId !== 1}" @click="houseId === 1 ? houseId = null : houseId = 1"><img src="../static/assets/snake.png"></div>
            <div class="select" :class="{houseSelected : houseId === 2, houseUnselected : houseId !== null && houseId !== 2}" @click="houseId === 2 ? houseId = null : houseId = 2"><img src="../static/assets/lion.png"></div>
          </div>
          <div class="input-control">
            <div class="select" :class="{houseSelected : houseId === 3, houseUnselected : houseId !== null && houseId !== 3}" @click="houseId === 3 ? houseId = null : houseId = 3"><img src="../static/assets/badger.png"></div>
            <div class="select" :class="{houseSelected : houseId === 4, houseUnselected : houseId !== null && houseId !== 4}" @click="houseId === 4 ? houseId = null : houseId = 4"><img src="../static/assets/eagle.png"></div>
          </div>
          <div class="input-control">
            <button type="button" class="input-submit" style="margin: auto;" @click="register()">Sign Up</button>
          </div>
        </form> -->

  <main class="signUpMain">
    <div class="signUpBlock">
      <svg fill="#242424" @click="$emit('select', null)" version="1.1" id="Capa_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" 
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
      <img v-if="houseId === 1" src="../static/assets/snake.png" alt="">
      <img v-if="houseId === 2" src="../static/assets/eagle.png" alt="">
      <img v-if="houseId === 3" src="../static/assets/badger.png" alt="">
      <img v-if="houseId === 4" src="../static/assets/lion.png" alt="">
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
          this.$toasted.show('You have registered successfully', {
            theme: 'primary',
            position: 'top-center',
            duration: 5000,
            type: 'success',
          })
          this.$router.push('/auth/login')
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

</style>