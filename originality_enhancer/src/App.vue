<template>
  <v-app>
    <v-app-bar app clipped-left color="primary">
      <div class="d-flex align-center" style="color: white">
        <v-icon large class="mr-4" style="color: white">mdi-compass-rose</v-icon>
        <h1>В жопу раз или вилкой в глаз??</h1>
        <v-icon large class="ml-4" style="color: white">mdi-compass-rose</v-icon>
      </div>
    </v-app-bar>

    <v-main>
      <router-view/>
    </v-main>
  </v-app>
</template>

<script>

export default {
  name: 'App',

  data: () => ({
    //
  }),
};
</script>
