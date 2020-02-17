<template>
  <v-app>
    <v-app-bar
      app
      color="#3c8dbe"
      dark
      height=55
    >
    </v-app-bar>

    <v-content>
      <Sample/>
    </v-content>
  </v-app>
</template>

<script>
import Sample from './components/Sample';

export default {
  name: 'App',

  components: {
    Sample,
  },

  data: () => ({
    //
  }),
};
</script>

<style lang="scss">
  main {
    background-color: #f2f3f5;
  }
</style>
