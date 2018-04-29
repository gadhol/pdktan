<template>
  <div class="layout-padding">
    <q-field
        icon="account_circle"
        label="Account"
        :count="4"
        :error="error2"
        helper="Masukkan kode aktivasi yang terkirim dinomor"
        error-label="Hey, we got an error">
        <q-input color="pink-6" v-model="code" />
      </q-field>
  </div>
</template>
<script>
/* eslint-disable */
import axios from 'axios'
axios.defaults.withCredentials = true;

import {
  QField,
  QInput
} from 'quasar'
export default {
  components: {
    QField,
    QInput
  },
  data() {
    return {
      code: ''
    }
  }
}
</script>
