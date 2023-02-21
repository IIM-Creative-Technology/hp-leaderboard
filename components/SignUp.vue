<template>
    <div style="background-image:../static/assets/hp.jpg ;">
        <form @submit="register()" enctype="multipart/form-data" method="post">
          <div class="names">
            <div class="name">
              <label for="firstname"><strong>First Name</strong></label>
              <input type="text" name="firstname" v-model="firstname" />
            </div>
            <div class="name">
              <label for="lastname"><strong>Last Name</strong></label>
              <input type="text" name="lastname" v-model="lastname" />
            </div>
          </div>
          <div class="fields">
            <label for="email"><strong>Email Address</strong></label>
            <input type="email" name="email" v-model="email" />

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
    </div>
    
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      firstname: '',
      lastname: '',
      email: '',
      password: '',
      error: null,
    }
  },

  methods: {
    async register() {
        console.log("le boss");
      const data = {
        firstname: this.firstname,
        lastname: this.lastname,
        email: this.email,
        password: this.password,
      }
      axios
        .post('localhost:3000/auth/register', data)
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