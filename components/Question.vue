<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
        <v-card>
          <v-card-title class="headline">
            {{ question.question }}
          </v-card-title>
          <v-card-text>
            <v-card class="mx-auto" max-width="500">
              <v-list shaped>
                <v-list-item-group>
                  <template>
                    <v-list-item
                      :value="question.question"
                      active-class="success"
                    >
                      <template v-slot:default="{ active }">
                        <v-list-item-content  v-for="opt in question.options" :key="opt">
                          <v-list-item-title>
                            {{ opt }}
                          </v-list-item-title>

                        <!-- <v-list-item-action> -->
                          <v-checkbox
                            :input-value="active"
                            color="success"
                          ></v-checkbox>
                        </v-list-item-content>
                        <!-- </v-list-item-action> -->
                      </template>
                    </v-list-item>
                  </template>
                </v-list-item-group>
              </v-list>
            </v-card>
          </v-card-text>
        </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  data: () => ({
    arrays: [],
  }),
  mounted () {
    console.log('rubbuish', this.question)
  },
  props: {
    question: {
      type: Object,
      default: () => {}
    }
  },
}
</script>
