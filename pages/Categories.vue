<template>
    <v-row justify="center">
    <v-col
      cols="12"
      sm="7"
      md="6"
      lg="5"
    >
      <v-card
    class="mx-auto"
    max-width="800"
  >
    



    <v-card-text>
      <h2 class="title mb-2">
        Choose A Category
      </h2>

      <v-chip-group
    
        column
        multiple
      >
        <v-chip
        v-for="category in categories"
              :key="category.id"
              @click="showCategory(category.id)"
          filter
          outlined
        >
         {{category.name}}
        </v-chip>
       
      </v-chip-group>
    </v-card-text>
  </v-card>

      <!-- <v-sheet
        elevation="10"
        rounded="xl"
      >
        

        <div class="pa-4">
          <v-chip-group
            active-class="primary--text"
            column
          >
            <v-chip
              v-for="category in categories"
              :key="category.id"
            >
              {{ category.name }}
            </v-chip>
          </v-chip-group>
        </div>
      </v-sheet> -->
    </v-col>
  </v-row>
  
</template>
<script>
export default {
    components:{

    },
     data: () => ({
   categories: {},
    
  }),
  async fetch () {
    try {
      let response = await this.$axios.$get(
        "https://opentdb.com/api_category.php"
      )
     this.categories = response.trivia_categories
    
   return {
         categories : response.trivia_categories
        }
      
    } catch (err) {
      console.log(err)
    }
  },
  methods: {
      showCategory(category){
        //   this.$router.push({ query: Object.assign({}, this.$route.query, {category: category}) });
         this.$router.push({ path: '/test', query: { category: category}})


      }
  }
}
</script>