<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8">
      <div class="text-center"></div>
      <div>

        {{indexOfQuestion}}/{{ questionsFromApiFormatted.length }}
        <v-spacer></v-spacer>
        {{ score }}
      </div>

      <Question :question="questionToDisplay" v-on:correctAnswer="addScore"/>
      <v-card>
        <v-card-actions>
          <v-btn v-if="indexOfQuestion !== questionsFromApiFormatted.length"  color="primary" nuxt @click="nextQuestion"> Next </v-btn>
          <divider/>
          <v-btn v-if="indexOfQuestion === questionsFromApiFormatted.length" to="/score" color="success" nuxt @click="submit">Submit </v-btn>
        </v-card-actions>
      </v-card>
    </v-col>
  </v-row>
</template>
  

<script>
import Question from '../components/Question'

export default {
  components: {
    Question,
  },
  data: () => ({
    score: 0,
    questionsFromApiFormatted: [],
    questionToDisplay: {},
    indexOfQuestion: 0,
  }),
  async fetch() {
    try {
      let response = await this.$axios.$get(
        `https://opentdb.com/api.php?amount=20&$category=${this.$route.query.category}&type=multiple`
      )
      this.questionsFromApiFormatted = response.results.map((item) => {
        const arrayOfOptions = [...item.incorrect_answers, item.correct_answer]
        return {
          question: item.question,
          correct_answer: item.correct_answer,
          options: this.mixOptions(arrayOfOptions),
        }
      })
      this.questionToDisplay = this.questionsFromApiFormatted[
        this.indexOfQuestion
      ]
      console.log(this.questionToDisplay)
    } catch (err) {
      console.log(err)
    }
  },
  computed: {
    questionNow() {
      return this.questionToDisplay
    },
  },
  methods: {
    addScore () {
      this.score++
    },
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
    
        this.questionToDisplay = this.questionsFromApiFormatted[
          this.indexOfQuestion++
        ]
        console.log(this.questionToDisplay)
      },
    
 
  },
}
</script>
