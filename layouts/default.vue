<template>
  <v-app dark>  
    <v-app-bar
      :clipped-left="clipped"
      fixed
      app
    >
    
      <v-toolbar-title v-text="title" />
      <v-spacer />
      <v-btn
      rounded
      color="primary"
      dark
      to="/"
    >
     Home
    </v-btn>
      
      <v-row
    align="center"
    justify="space-around"
  >
   
   <div class="text-center">
    <v-btn
      rounded
      color="primary"
      dark
      to="/categories"
    >
      Categories
    </v-btn>
  </div>
  </v-row>
    </v-app-bar>
    <v-main>
      <v-container>
        <nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      clipped: false,
      title: 'TRIVIA QUIZ APP'
    }
  }
}
</script>
