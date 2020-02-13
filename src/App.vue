<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
      height=4
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
