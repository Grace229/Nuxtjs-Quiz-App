<template>
  <v-row justify="center" align="center">
    <v-card>
      <v-card-title class="headline">
        <div v-html="question.question">
        </div>
      </v-card-title>
      <v-card-text>
        <v-card class="mx-auto">
          <v-list shaped>
            <v-list-item-group>
              <template>
                <v-list-item
                  :value="opt"
                  active-class="success"
                  v-for="(opt, i) in question.options"
                  :key="`opt-${i}`"
                >
                  <template v-slot:default="{ active }">
                    <v-list-item-content>
                      <v-list-item-title>
                        {{ opt }}
                      </v-list-item-title>
                    </v-list-item-content>

                    <v-checkbox
                      :input-value="active"
                      color="success"
                      @click="selectOption(opt)"
                    ></v-checkbox>
                  </template>
                </v-list-item>
              </template>
            </v-list-item-group>
          </v-list>
        </v-card>
      </v-card-text>
    </v-card>
  </v-row>
</template>

<script>
export default {
  data: () => ({}),
  mounted() {
    console.log('rubbuish', this.question.options)
  },
  props: {
    question: {
      type: Object,
      default: () => {},
    },
  },
  methods: {
    selectOption (value) {
     const optionSelect =  {
       selectedAnswer: value,
       correctAnswer: this.question.correct_answer 
     }
      this.$emit('optionSelectEmit', optionSelect)
    }
  }
}
</script>
