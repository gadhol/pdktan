<template>
  <div>

    <q-toolbar color="pink-6">
      <q-toolbar-title class="text-center" style="font-family:pacifico">Pdktan</q-toolbar-title>
    </q-toolbar>

    <router-view></router-view>

    <q-tabs v-show="this.$session.exists()" align="center" class="fixed-bottom" color="pink-6">
      <q-route-tab
        icon="ion-ios-person-outline"
        name="tab-profile"
        to="/profile"
        slot="title"
        />
      <q-route-tab
        icon="ion-ios-circle-outline"
        name="tab-discover"
        to="/discover"
        slot="title"
      />
      <q-route-tab
        icon="ion-ios-heart-outline"
        name="tab-activity"
        to="/activity"
        slot="title" 
        />
    </q-tabs>
    
  </div>
</template>
<script>
/* eslint-disable */
import { AddressbarColor, QTabs, QRouteTab, QToolbar, QToolbarTitle } from 'quasar'
AddressbarColor.set('#e91e63')
export default {
  components: {
    QTabs,
    QRouteTab,
    QToolbar,
    QToolbarTitle
  },
  data () {
    return {
    }
  },
  methods: {
    keluar(){
      axios.get('https://pdktan-api.herokuapp.com/logout', function() {
        alert('berhasil')
      })
      this.$session.destroy()
      this.$router.push('/')
    }
  }
}
</script>