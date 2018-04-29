<template>
  <div class="layout-padding">
    <h1>{{this.dataDiri.nama}}</h1>
    <Upload action="https://pdktan-api-iwic.herokuapp.com/unggahFoto" name="unggahFoto" :with-credentials="true">
        <Button type="ghost" icon="ios-cloud-upload-outline">Unggah Foto</Button>
    </Upload>
    <img :src="this.dataDiri.foto" class="responsive"/>
    <q-btn id="btn" color="pink-6" @click="keluar">keluar</q-btn>
  </div>
</template>

<script>
/* eslint-disable */
import axios from 'axios'
axios.defaults.withCredentials = true;

import {QBtn, Toast, QUploader} from 'quasar'

export default {
  components: {
    QBtn,
    Toast,
    QUploader
  },
  beforeCreate: function () {
    if (!this.$session.exists()) {
        this.$router.push('/')
    }
  },
  data() {
    return {
      dataDiri: {}
    }
  },
  mounted() {
    axios
      .get('https://pdktan-api-iwic.herokuapp.com/profile')
      .then((response) => {
        this.dataDiri = response.data;
      })
  },
  methods: {
    keluar(){
      Toast.create('Berhasil keluar')
      axios.get('https://pdktan-api-iwic.herokuapp.com/logout')
      this.$session.destroy()
      this.$router.push('/')
    }
  }
}
</script>

<style scoped>
#btn {
  font-family: 'Montserrat', sans-serif;
  font-weight: 700;
  margin-top: 20px;
  margin-bottom: 50px;
  border-radius: 100px;
  line-height: 30px;
  font-size:22px;
  width: 100%;
  padding: 30px;
}
</style>
