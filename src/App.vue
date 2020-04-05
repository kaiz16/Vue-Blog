<template>
  <v-app>
      <v-content>
        <app-main v-on:hideProgress="showProgressCircle = $event"></app-main>
        <Progress v-show="showProgressCircle"/>
      </v-content>
      <bottom-nav/>
  </v-app>
</template>

<script>

import Nav from '@/components/BottomNav.vue'
import Main from '@/components/Main.vue'
import Progress from '@/components/Progress.vue'

export default {
  name: 'App',
  components: {
    'bottom-nav': Nav,
    'app-main': Main,
      Progress,
  },
  data: () => ({
    showProgressCircle: true
  })
}
</script>
