<template>
    <nav>
        <v-bottom-navigation fixed="" app>
          <v-btn value="recent">
            <span>Blogs</span>
            <v-icon>mdi-format-list-bulleted</v-icon>
          </v-btn>

          <v-btn value="favorites">
            <span>Favorites</span>
            <v-icon>mdi-heart</v-icon>
          </v-btn>

          <v-btn value="nearby">
            <span>Nearby</span>
            <v-icon>mdi-map-marker</v-icon>
          </v-btn>
        </v-bottom-navigation>
    </nav>

</template>

<script>
export default {
  data: function () {
    return {
      drawer: false
    }
  }

}
</script>
<style scoped>
.v-btn {
  min-height: 100%;
}
</style>