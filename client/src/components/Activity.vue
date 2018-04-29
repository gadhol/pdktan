
<template>
  <div class="layout-padding row justify-center">
    <div style="width: 500px; max-width: 90vw;">
      <q-list highlight>
        <q-list-header>Naksir Kamu</q-list-header>
        <q-item v-for="naksirResult in naksirResults" :key="naksirResult._id">
          
          <q-item-side>
            <q-item-tile avatar>
              <img v-if="typeof naksirResult.foto == 'undefined'" src="https://ssl.gstatic.com/images/branding/product/1x/avatar_circle_blue_512dp.png">
              <img v-if="typeof naksirResult.foto != 'undefined'" :src="naksirResult.foto">
            </q-item-tile>
          </q-item-side>

          <q-item-main>
            <q-item-tile label>{{naksirResult.nama}}</q-item-tile>
            <q-item-tile sublabel>{{naksirResult.kelas}} {{naksirResult.jurusan}}</q-item-tile>
            <q-item-tile sublabel >ID LINE: {{naksirResult.line}}</q-item-tile>
          
          </q-item-main>

          <q-item-side right v-for="ratingResult in naksirResult.naksir" :key="ratingResult.id">
            <q-rating v-if="ratingResult.id == dataDiri.userId && typeof ratingResult.id != 'string'" v-model="ratingResult.rating" :max="5" size="1.5rem" color="pink-6" icon="ion-ios-heart-outline" readonly/>
          </q-item-side>


        </q-item>

        <q-item-separator />

        <q-list-header>Berjodoh</q-list-header>
        <q-item v-for="jodohResult in jodohResults" :key="jodohResult._id">
          
          <q-item-side>
            <q-item-tile avatar>
              <img v-if="typeof jodohResult.foto == 'undefined'" src="https://ssl.gstatic.com/images/branding/product/1x/avatar_circle_blue_512dp.png">
              <img v-if="typeof jodohResult.foto != 'undefined'" :src="jodohResult.foto">
            </q-item-tile>
          </q-item-side>

          <q-item-main>
            <q-item-tile label>{{jodohResult.nama}}</q-item-tile>
            <q-item-tile sublabel>{{jodohResult.kelas}} {{jodohResult.jurusan}}</q-item-tile>
            <q-item-tile sublabel>ID LINE: {{jodohResult.line}}</q-item-tile>
            <q-item-tile sublabel >No HP: {{jodohResult.hp}}</q-item-tile>
          </q-item-main>

        </q-item>

      </q-list>
    </div>
  </div>
</template>

<script>
/* eslint-disable */
import axios from "axios";
axios.defaults.withCredentials = true;

import {
  QList,
  QListHeader,
  QItem,
  QItemSeparator,
  QItemSide,
  QItemMain,
  QRating,
  QItemTile
} from "quasar";

export default {
  components: {
    QList,
    QListHeader,
    QItem,
    QItemSeparator,
    QItemSide,
    QItemMain,
    QRating,
    QItemTile
  },
  data() {
    return {
      naksirResults: [],
      jodohResults: [],
      dataDiri: {}
    };
  },
  beforeCreate: function() {
    if (!this.$session.exists()) {
      this.$router.push("/");
    }
  },
  mounted() {
    axios
      .get("https://pdktan-api-iwic.herokuapp.com/cariYangNaksir")
      .then(response => {
        console.log("yang naksir: ", response);
        this.naksirResults = response.data;
      })
      .catch(err => {
        console.error(err);
      });

    axios
      .get("https://pdktan-api-iwic.herokuapp.com/cariYangJodoh")
      .then(response => {
        console.log("yang jodoh: ", response)
        this.jodohResults = response.data
      })
      .catch(err => {
        console.error(err)
      });

    axios
      .get('https://pdktan-api-iwic.herokuapp.com/profile')
      .then((response) => {
        this.dataDiri = response.data
      })
  }
};
</script>
