<template>
  <div class="heading">
    <div class="layout-padding">
      <q-carousel autoplay infinite style="margin-top: -50px; margin-bottom: -55px; margin-left: -50px;">
        <div slot="slide">
          <h2 style="font-size:50px">Suka sama doi Tapi cuma bisa ngeliatin dari jauh.</h2>
        </div>
        <div slot="slide">
          <h2>Takut ke GRan kalau dia suka sama lu.</h2>
        </div>
      </q-carousel>
      <q-btn id="btn" color="pink-6" @click="$router.push('/register')">Bikin peka sekarang</q-btn>
      <q-btn id="btn" color="white" class="text-pink-6" @click="$router.push('/login')">Masuk</q-btn>
    </div>
  </div>
</template>
<script>
/* eslint-disable */
import { QBtn, QCarousel } from 'quasar'

export default {
  components: {
    QBtn,
    QCarousel
  },
  beforeCreate: function () {
    if (this.$session.exists()) {
        this.$router.push('/discover')
    }
  },
}
</script>

<style scoped>

.heading {
  height: 100vh;
  background-image: linear-gradient(to bottom, #ed6ea0 0%, #ec8c69 100%);
  background-position: center center;
	background-repeat: no-repeat;
	background-attachment: fixed;
	background-size: cover;
}

.heading h2 {
  color: white;
  font-family: 'Montserrat', sans-serif;
  font-weight: 700;
  padding-left: 30px;
  margin-top:-5px;
}

#btn {
  font-family: 'Montserrat', sans-serif;
  font-weight: 700;
  margin-top: 20px;
  margin-bottom: 0px;
  border-radius: 100px;
  font-size:22px;
  width: 100%;
  padding: 20px;
}

</style>
