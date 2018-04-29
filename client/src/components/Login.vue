<template>
  <div class="layout-padding">
    <q-input color="pink-6" v-model="User.username" type="text" float-label="Username/ID" clearable />
    <q-input color="pink-6" v-model="User.password" type="password" float-label="Password" />
    <q-btn loader class="customCSS" @click="masuk" outline color="pink-6">Masuk</q-btn>
    <p @click="$router.push('/register')" class="text-pink-6">Belum mempunyai akun? Daftar</p>
  </div>
</template>

<script>
/* eslint-disable */
import axios from 'axios'
axios.defaults.withCredentials = true;
import {QInput, QBtn, Toast} from 'quasar'

export default {
  beforeCreate: function () {
    if (this.$session.exists()) {
        this.$router.push('/discover')
    }
  },
  components: {
    QInput,
    QBtn,
    Toast
  },
  data() {
    return {
      User: {
        username: '',
        password: ''
      }
    }
  },
  methods: {
    simulateProgress (e, done) {
      setTimeout(done, 3000)
    },
    masuk(){
      const loginUser = {
        username: this.User.username.split(' ').join('').toLowerCase(),
        password: this.User.password
      }
      axios.post('https://pdktan-api-iwic.herokuapp.com/login', loginUser)
        .then(response => {
          console.log(response)
          this.result = response.data[0]
          if (response.data.length == 0) {
            alert('email/password salah')
          } else {
            Toast.create(`Halo ${response.data[0].nama}`)
            this.$session.start()
            this.$router.push('/discover')
          }
        })
        .catch(err => {
          console.error(err)
        })
    }
  }
};
</script>

<style scoped>
  .customCSS {
    margin-bottom: 30px;
    margin-top: 20px;
  }
</style>