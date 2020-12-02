<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <div class="text-center">
      
      </div>
      <v-container v-if="loading">
    <div class="text-xs-center">
      <v-progress-circular
        indeterminate
        :size="150"
        :width="8"
        color="green">
      </v-progress-circular>
    </div>
  </v-container>
  <v-container v-else>
     <v-card v-for="(data, i) in datas" :key="data.id">
        <v-card-title class="headline">
          {{data.question}}
        </v-card-title>
        <v-card-text>
          <v-card 
    class="mx-auto"
    max-width="500"
  >
    <v-list shaped>
      <v-list-item-group
      >
        <template>
        

          <v-list-item
           
            :key="`data-${i}`"
            :value="data"
            active-class="success"
          >
            <template v-slot:default="{ active }">
              <v-list-item-content>
                <v-list-item-title >
                  {{data.correct_answer}}
                </v-list-item-title>
              </v-list-item-content>

              <v-list-item-action>
                <v-checkbox
                  :input-value="active"
                  color="success"
                ></v-checkbox>
              </v-list-item-action>
              
              
            </template>
            
          </v-list-item>

        </template>
      </v-list-item-group>
    </v-list>
        <v-list shaped>
      <v-list-item-group
      >
        <template>
        

          <v-list-item
           
            :key="`data-${i}`"
            :value="data"
            active-class="success"
          >
            <template v-slot:default="{ active }">
              <v-list-item-content>
                <v-list-item-title >
                  <!-- {{data.correct_answer}} -->
                </v-list-item-title>
              </v-list-item-content>

              <v-list-item-action>
                <v-checkbox
                  :input-value="active"
                  color="success"
                ></v-checkbox>
              </v-list-item-action>
              
              
            </template>
            
          </v-list-item>

        </template>
      </v-list-item-group>
    </v-list>
  </v-card>
        </v-card-text>
      

      </v-card>
      </v-container>
    </v-col>
  </v-row>
</template>

<script>


export default {
  components: {
  
  },
      data: () => ({
      arrays:[]
    }),

   props: {

    loading: {
      default: false
    },
  },
  async asyncData({ $axios }){
    try {
      let response = await $axios.$get('https://opentdb.com/api.php?amount=20&category=9&type=multiple');
        
      return{
       datas: response.results,
    
      }
       this.arrays = response.results.incorrect_answers
 console.log(arrays)
    
    } catch (err) {
      console.log(err)
    }
  }
}
</script>
