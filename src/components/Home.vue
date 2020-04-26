<template>
<div class="spaceBackground">

<v-row>
  <v-container>
  <!-- Apollo watched Graphql query -->
  <ApolloQuery :query="require('../graphql/AllGalaxies.gql')"
   :variables="{ searchString }">

    <template v-slot="{ result: { loading, error, data } }">
      <!-- Loading -->
      <div v-if="loading" class="loading apollo">Loading...</div>

      <!-- Error -->
      <div v-else-if="error" class="error apollo">An error occured</div>

      <!-- Result -->
      
      <div v-else-if="data" class="result apollo">
        <h1>GraphQl Query All</h1>
        <v-row>
          <v-col cols="3" v-for="(item, i) in data.Galaxy" :key="i">
            <v-card class="mx-auto" max-width="350">
              <v-card-text>
                <p>ID: {{ item.id }}</p>
                <p>Cateogry: {{ item.category }}</p>
                <p>Name: <strong>{{ item.name }}</strong></p>
                <p>Constellation: {{ item.constellation }}</p>
                <p>Name Origin: {{ item.nameOrigin }}</p>
                <p>Distance from Milky Way (In millions of light years): {{ item.distance }}</p>
              </v-card-text>
            </v-card>
          </v-col>
        </v-row>
      </div>

      <!-- No result -->
      <div v-else class="no-result apollo">No result :(</div>
    </template>
  </ApolloQuery>
  </v-container>
</v-row>



<!-- trying to get single query to work here --> 

  <!-- <ApolloQuery :query="require('../graphql/GetPerson.gql')"
   :variables="{ id }">
    <template v-slot="{ query, result: { loading, error, data } }">
      <v-form>
        <v-container>
          <v-card-title>Get a Person</v-card-title>
          <v-row>
            <v-col cols="6" md="6">
              <v-text-field v-model="id" label="id" required filled></v-text-field>
            </v-col>
          </v-row>        
          <v-btn large color="primary" :disabled="loading" @click="query()">Get Person</v-btn>
          <p v-if="error">An error occurred: {{ error }}</p>
        </v-container>
      </v-form>
-->

      <!-- Loading -->
      <!-- <div v-if="loading" class="loading apollo">Loading...</div> -->

      <!-- Error -->
      <!-- <div v-else-if="error" class="error apollo">An error occured</div> -->

      <!-- Result -->
      <!-- <div v-else-if="data" class="result apollo">
        <v-row>
            <v-card class="mx-auto" max-width="350">
              <v-card-text>
                <p class="name">
                  {{ Person.name }}
                </p>
                <p>{{ Person.age }}</p>
              </v-card-text>
            </v-card>
        </v-row>
      </div> -->

      <!-- No result -->
<!--       <div v-else class="no-result apollo">No result :(</div>
    </template>
  </ApolloQuery> -->
</div>
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
h1 {
  color: white;
  margin-bottom: 30px;
}
.name {
  font-size: 1.25rem;
  font-weight: 600;
}
.spaceBackground {
  background-image: url('../assets/stars2.jpg');
  height: 100%;
  background-repeat: repeat-y;
}
</style>
