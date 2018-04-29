<template>
  <div>
    <q-carousel arrows infinite class="text-white" style="height:90vh">
      <div v-for="result in results" :key="result._id" slot="slide">
        <Card class="fixed-center" style="max-width: 600px; margin: auto">
          <p v-if="typeof result.foto == 'undefined'" slot="title" style="background-image: linear-gradient(to right, #ed6ea0 0%, #ec8c69 100%); height:300px;"></p>
          <img v-if="typeof result.foto != 'undefined'" class="responsive" :src="result.foto" slot="title"/>
          <h6 class="text-white" slot="title" style="margin-left: 10px;margin-top:-55px; font-family: Montserrat; font-weight: 400;"><b>{{result.nama}}</b><br> {{result.kelas}} {{result.jurusan}}</h6>
          <q-rating @change="klikNaksir(result)" size="2rem" color="pink-6" v-model="User.rating" :max="5" icon="ion-ios-heart-outline" />
        </Card>
      </div>
    </q-carousel>
  </div>
</template>

<script>
/* eslint-disable */
import axios from "axios";
axios.defaults.withCredentials = true;
import {
  QBtn,
  QCarousel,
  QCard,
  QCardMain,
  QCardTitle,
  QCardSeparator,
  QRating,
  Toast
} from "quasar";
export default {
  beforeCreate: function() {
    if (!this.$session.exists()) {
      this.$router.push("/");
    }
  },
  components: {
    QBtn,
    QCarousel,
    QCard,
    QCardTitle,
    QCardSeparator,
    QCardMain,
    QRating,
    Toast
  },
  data() {
    return {
      results: [],
      User: {
        naksir: "",
        hp: "",
        rating: ""
      }
    };
  },
  mounted() {
    axios
      .get("https://pdktan-api-iwic.herokuapp.com/caripasangan")
      .then(response => {
        console.log(response);
        this.results = response.data;
      })
      .catch(err => {
        console.error(err);
      });
  },
  methods: {
    klikNaksir(result) {
      this.User.naksir = result._id;
      this.User.hp = result.hp;
      Toast.create(`Kamu naksir ${result.nama}`);
      const newNaksir = {
        naksir: {
          id: this.User.naksir,
          rating: this.User.rating
        },
        hp: this.User.hp
      };

      axios
        .post("https://pdktan-api-iwic.herokuapp.com/kliknaksir", newNaksir)
        .then(response => {
          alert("berhasil naksir ke" + newNaksir);
        })
        .catch(err => {
          console.error(err);
        });
    }
  }
};
</script>

