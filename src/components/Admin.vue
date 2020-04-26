<template>
<div class="spaceBackground">





    <v-row>
      <v-col>
        <h1>Search</h1><br>
        <v-text-field v-model="searchString" label="Search for an item..."></v-text-field>
      </v-col>
    </v-row>
  <!-- Apollo watched Graphql query -->
  <ApolloQuery :query="require('../graphql/SearchGalaxy.gql')"
   :variables="{ searchString }">
    <template v-slot="{ result: { loading, error, data } }">
      <!-- Loading -->
      <div v-if="loading" class="loading apollo">Loading...</div>

      <!-- Error -->
      <v-alert type="error" v-else-if="error" class="error apollo">An error occured</v-alert>

      <!-- Result -->
      <div v-else-if="data" class="result apollo">        
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



<!-- CREATE ITEM -->
  <ApolloMutation
    :mutation="require('../graphql/AddGalaxy.gql')"
    :variables="{
      createCategory,
      createName,
      createConstellation,
      createNameOrigin,
      createDistance
      }"
      @done="onDone"
  >
    <template v-slot="{ mutate, loading, error }">
      <!-- Form here -->
      <v-form>
        <v-container>
          <h1>GraphQl CRUD</h1>
          
          <v-card-title>Create an Item</v-card-title>
          <v-row>
            <v-col cols="6" md="6">
              <v-text-field v-model="createCategory" label="category" required filled></v-text-field>
            </v-col>
            <v-col cols="6" md="6">
              <v-text-field v-model="createName" label="name" rows="4" required filled></v-text-field>
            </v-col>
            <v-col cols="6" md="6">
              <v-text-field v-model="createConstellation" label="constellation" rows="4" required filled></v-text-field>
            </v-col>
            <v-col cols="6" md="6">
              <v-text-field v-model="createNameOrigin" label="name origin" rows="4" required filled></v-text-field>
            </v-col>
            <v-col cols="6" md="6">
              <v-text-field v-model="createDistance" label="distance" rows="4" required filled></v-text-field>
            </v-col>
          </v-row>        
          <v-btn large class="button"  :disabled="loading" @click="mutate()">Add Item</v-btn>
          <p v-if="error">An error occurred: {{ error }}</p>
        </v-container>
      </v-form>
    </template>
  </ApolloMutation>

<!-- UPDATE PERSON -->
<ApolloMutation
      :mutation="require('../graphql/UpdateGalaxy.gql')"
      :variables="{
        id,
        category,
        name,
        constellation,
        nameOrigin,
        distance
        }"
        @done="onDone"
    >
      <template v-slot="{ mutate, loading, error }">
        
        <!-- Form here -->
        <v-form color="#ffffff">
          <v-container>
            <v-card-title>Update an Item</v-card-title>
            <v-row>
              <v-col cols="4" md="4">
                <v-text-field v-model="id" label="id" required filled></v-text-field>
              </v-col>
              <v-col cols="4" md="4">
                <v-text-field v-model="category" label="category" required filled></v-text-field>
              </v-col>
              <v-col cols="4" md="4">
                <v-text-field v-model="name" label="name" required filled></v-text-field>
              </v-col>
              <v-col cols="4" md="4">
                <v-text-field v-model="constellation" label="constellation" required filled></v-text-field>
              </v-col>
              <v-col cols="4" md="4">
                <v-text-field v-model="nameOrigin" label="name origin" required filled></v-text-field>
              </v-col>
              <v-col cols="4" md="4">
                <v-text-field class="form" v-model="distance" label="distance" required filled></v-text-field>
              </v-col>
            </v-row>
          
            <v-btn large class="button" :disabled="loading" @click="mutate()">Update Item</v-btn>
            <p v-if="error">An error occurred: {{ error }}</p>
          </v-container>
        </v-form>
      </template>
    </ApolloMutation>



<!-- DELETE PERSON -->
    <ApolloMutation
      :mutation="require('../graphql/RemoveGalaxy.gql')"
      :variables="{
        removeId,
        }"
        @done="onDone"
    >
      <template v-slot="{ mutate, loading, error }">
        
        <!-- Form here -->
        <v-form>
          <v-container>
            <v-card-title>Delete an Item</v-card-title>
            <v-row>
              <v-col cols="12" md="12">
                <v-text-field class="form" v-model="removeId" label="id" required filled></v-text-field>
              </v-col>
            </v-row>
          
            <v-btn large class="button" :disabled="loading" @click="mutate()">Delete Item</v-btn>
            <p v-if="error">An error occurred: {{ error }}</p>
          </v-container>
        </v-form>
      </template>
    </ApolloMutation>
  </div>
</template>


<style scoped>
h1 {
  color: #FF19B3;
}
button {
  color: white !important;
  background-color: #FF19B3 !important;
}
/*
.spaceBackground {
  // background-image: url('../assets/stars1.jpg');
  height: 100%;
  background-repeat: repeat-y;
  padding-bottom: 50px;
}
 .form {
  background-color: white;
}
v-input__slot {
  margin-bottom: 0;
}
v-text-field__details {
  display: none;
} */
</style>

<script>
export default {
   data: () => ({
    searchString: "Milky Way",
    idInput: '',

    createCategory: '',
      createName: '',
      createConstellation: '',
      createNameOrigin: '',
      createDistance: '',

      id: '',
      category: '',
      name: '',
      constellation: '',
      nameOrigin: '',
      distance: '',

      removeId: '',
  }),

  methods: {
    onDone() {
      return console.log('Done' + 'did it work?')
    }
  }
}
</script>