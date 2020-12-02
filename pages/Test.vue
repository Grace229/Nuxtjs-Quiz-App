<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <div class="text-center"></div>
      <v-card>
        <v-card-actions>
          <v-btn color="success" nuxt @click="prevQuestion"> Previous </v-btn>
          <v-spacer />
          <v-btn color="primary" nuxt @click="nextQuestion"> Next </v-btn>
        </v-card-actions>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  components: {},
  data: () => ({
    arrays: [],
  }),

  props: {
    loading: {
      default: false,
    },
  },
  async asyncData({ $axios }) {
    try {
      let response = await $axios.$get(
        'https://opentdb.com/api.php?amount=20&category=9&type=multiple'
      )
console.log("response", response)
      return {
        datas: response.results,
      }
     
    } catch (err) {
      console.log(err)
    }
  },
  methods: {
    nextQuestion ()
  }
}
</script>
