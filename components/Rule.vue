<template>
  <div class="App">
     <v-card>
        <v-card-title class="headline">
          Welcome to the Vuetify + Nuxt.js template
        </v-card-title>
        <v-card-text>
          <p>Vuetify is a progressive Material Design component framework for Vue.js. It was designed to empower developers to create amazing applications.</p>
          <p>
            For more information on Vuetify, check out the.
          </p>
          <p>
            If you have questions, please join the official 
              .
          </p>
          <p>
            Find a bug? Report it on the github.
          </p>
          <p>Thank you for developing with Vuetify and I look forward to bringing more exciting features in the future.</p>
          <div class="text-xs-right">
            <em><small>&mdash; John Leider</small></em>
          </div>
          <hr class="my-3">
        </v-card-text>
        <v-card-actions>
          <v-spacer />
          <v-btn
            color="primary"
            nuxt
            to="/test"
          >
            Take a test
          </v-btn>
        </v-card-actions>
      </v-card>
  </div>
</template>

<style>

</style>
