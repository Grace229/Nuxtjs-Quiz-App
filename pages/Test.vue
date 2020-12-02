<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <div class="text-center">
        <Question :question="questionToDisplay" />
      </div>
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
import Question from '../components/Question'

export default {
  components: {
    Question
  },
  data: () => ({
    questionsFromApiFormatted: [],
    questionToDisplay: {},
    indexOfQuestion: 0
  }),
  async fetch () {
    try {
      let response = await this.$axios.$get(
        `https://opentdb.com/api.php?amount=20&$category=${9}&type=multiple`
      )
      this.questionsFromApiFormatted = response.results.map((item) => {
        const arrayOfOptions = [...item.incorrect_answers, item.correct_answer]
        return {
          question: item.question,
          correct_answer: item.correct_answer,
          options: this.mixOptions(arrayOfOptions),
        }
      })
      this.questionToDisplay = this.questionsFromApiFormatted[0]
      console.log(this.questionToDisplay)
    } catch (err) {
      console.log(err)
    }
  },
  computed: {
    questionNow () {
      return this.questionToDisplay
    }
  },
  methods: {
    mixOptions(array) {
      var currentIndex = array.length,
        temporaryValue,
        randomIndex

      // While there remain elements to shuffle...
      while (0 !== currentIndex) {
        // Pick a remaining element...
        randomIndex = Math.floor(Math.random() * currentIndex)
        currentIndex -= 1

        // And swap it with the current element.
        temporaryValue = array[currentIndex]
        array[currentIndex] = array[randomIndex]
        array[randomIndex] = temporaryValue
      }
      return array
    },
    nextQuestion() {
      this.questionToDisplay = this.questionsFromApiFormatted[2]
      console.log(this.questionToDisplay)
    },
    prevQuestion() {
      console.log('next')
    },
  },
}
</script>
