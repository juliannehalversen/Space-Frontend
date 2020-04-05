<template>
  <!-- Apollo watched Graphql query -->
  <ApolloQuery :query="require('../graphql/AllPeople.gql')"
   :variables="{ searchString }">
    <template v-slot="{ result: { loading, error, data } }">
      <!-- Loading -->
      <div v-if="loading" class="loading apollo">Loading...</div>

      <!-- Error -->
      <div v-else-if="error" class="error apollo">An error occured</div>

      <!-- Result -->
      <div v-else-if="data" class="result apollo">
        <v-row>
          <v-col cols="3" v-for="(item, i) in data.People" :key="i">
            <v-card class="mx-auto" max-width="350">
              <v-card-text>
                <p class="name">
                  {{ item.name }}
                </p>
                <p>{{ item.age }}</p>
              </v-card-text>
            </v-card>
          </v-col>
        </v-row>
      </div>

      <!-- No result -->
      <div v-else class="no-result apollo">No result :(</div>
    </template>
  </ApolloQuery>
</template>

<script>
//import vue-truncate-filter from 'vue-truncate-filter'

export default {
  name: 'HelloWorld',

  data: () => ({
    searchString: "Test"
  }),
}
</script>

<style scoped>
.result {
  padding: 1rem;
}

.name {
  font-size: 1.25rem;
  font-weight: 600;
}
</style>
