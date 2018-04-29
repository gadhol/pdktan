<template>
  <div class="layout-padding">
    <h3 class="text-pink-6">Registrasi</h3>
    <q-input color="pink-6" v-model="User.nama" type="text" float-label="Nama" clearable />
    <q-input color="pink-6" v-model="User.username" type="text" float-label="Username/ID" clearable />
    <q-input color="pink-6" v-model="User.password" type="password" float-label="Password" clearable />
    <q-input color="pink-6" v-model="User.konfpassword" type="password" float-label="Konfirmasi Password" clearable/>
    <q-input color="pink-6" v-model="User.email" type="email" float-label="Email" clearable />
    <q-input color="pink-6" v-model="User.line" type="text" float-label="ID LINE" clearable />
    <q-input color="pink-6" v-model="User.hp" type="text" float-label="Nomor HP" clearable />
    <q-option-group
      type="radio"
      color="pink-6"
      v-model="User.kelamin"
      :options="[
        { label: 'Laki-laki', value: 'laki-laki' },
        { label: 'Perempuan', value: 'perempuan' }
      ]"
    />
    <q-datetime color="pink-6" v-model="User.tanggalLahir" type="date" float-label="Tanggal Lahir"/>
    <q-select
      float-label="Sekolah/Institusi"
      type="radio"
      color="pink-6"
      v-model="User.institusi"
      :options="[
        { label: 'SMK Telkom Jakarta', value: 'SMK Telkom Jakarta' }
      ]"
    />
    <q-input color="pink-6" v-model="User.kelas" type="text" float-label="Kelas" clearable />
    <q-input color="pink-6" v-model="User.jurusan" type="text" float-label="Jurusan" clearable />
    <q-btn loader class="customCSS"@click="daftar" outline color="pink-6">Daftar</q-btn>
    <p @click="$router.push('/login')" class="text-pink-6">Sudah mempunyai akun? Masuk</p>
  </div>
</template>

<script>
/* eslint-disable */
import axios from "axios";
axios.defaults.withCredentials = true;
import { QInput, QBtn, QOptionGroup, QSelect, QRadio, QDatetime, Toast } from "quasar";

export default {
  beforeCreate: function () {
    if (this.$session.exists()) {
        this.$router.push('/discover')
    }
  },
  components: {
    QInput,
    QBtn,
    QOptionGroup,
    QSelect,
    QRadio,
    QDatetime,
    Toast
  },
  data() {
    return {
      User: {
        nama: "",
        username: "",
        password: "",
        konfpassword: "",
        email: "",
        line: "",
        hp: "",
        kelamin: "",
        tanggalLahir: "",
        institusi: "",
        kelas: "",
        jurusan: ""
      }
    };
  },
  methods: {
    simulateProgress (e, done) {
      setTimeout(done, 3000)
    },
    daftar() {
      const newUser = {
        nama: this.User.nama,
        username: this.User.username.split(' ').join('').toLowerCase(),
        password: this.User.password,
        email: this.User.email.toLowerCase(),
        line: this.User.line,
        hp: this.User.hp,
        kelamin: this.User.kelamin,
        tanggalLahir: this.User.tanggalLahir,
        institusi: this.User.institusi,
        kelas: this.User.kelas,
        jurusan: this.User.jurusan
      };
      if (newUser.password == this.User.konfpassword) {
        axios
          .post("https://pdktan-api-iwic.herokuapp.com/register", newUser)
          .then(response => {
            console.log(response);
            Toast.create('Berhasil daftar!')
            this.$router.push('/login')
          })
          .catch(err => {
            console.error(err);
          });
      } else {
        Toast.create('Password dan Konfirmasi password tidak cocok')
      }
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
