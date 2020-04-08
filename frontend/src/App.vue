<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />

        <h2>
          Capstone
        </h2>
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/psnx"
        target="_blank"
        text
      >
        <span class="mr-2">Github/psnx</span>
        <v-icon>mdi-github</v-icon>
      </v-btn>

      <v-btn
        href="https://hub.docker.com/repository/docker/psnx/cloudnd-capstone/"
        target="_blank"
        text
      >
        <span class="mr-2-center">DockerHub/psnx/capstone</span>
        <v-icon>mdi-docker</v-icon>
      </v-btn>
    </v-app-bar>

    <v-content>
      <HelloWorld/>
    </v-content>
    <v-footer>
      <span class="mr-2"> Made with 
        <a href="https://vuejs.org">Vue</a> and 
        <a href="https://vuetifyjs.com/en/">Vuetify</a> 
      </span>
    </v-footer>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';

export default {
  name: 'App',

  components: {
    HelloWorld,
  },

  data: () => ({
    //
  }),
};
</script>
