<template>
<div>
<!-- CREATE PERSON -->
  <ApolloMutation
    :mutation="require('../graphql/AddPerson.gql')"
    :variables="{
      name,
      age
      }"
      @done="onDone"
  >
    <template v-slot="{ mutate, loading, error }">
      <!-- Form here -->
      <v-form>
        <v-container>
          <v-card-title>Create a Person</v-card-title>
          <v-row>
            <v-col cols="6" md="6">
              <v-text-field v-model="name" label="name" required filled></v-text-field>
            </v-col>
            <v-col cols="6" md="6">
              <v-text-field v-model="age" label="age" rows="4" required filled></v-text-field>
            </v-col>
          </v-row>        
          <v-btn large color="primary" :disabled="loading" @click="mutate()">Add Person</v-btn>
          <p v-if="error">An error occurred: {{ error }}</p>
        </v-container>
      </v-form>
    </template>
  </ApolloMutation>

<!-- UPDATE PERSON -->
<ApolloMutation
      :mutation="require('../graphql/UpdatePerson.gql')"
      :variables="{
        id,
        name
        }"
        @done="onDone"
    >
      <template v-slot="{ mutate, loading, error }">
        
        <!-- Form here -->
        <v-form>
          <v-container>
            <v-card-title>Update a Person</v-card-title>
            <v-row>
              <v-col cols="4" md="4">
                <v-text-field v-model="id" label="id" required filled></v-text-field>
              </v-col>
              <v-col cols="4" md="4">
                <v-text-field v-model="name" label="name" required filled></v-text-field>
              </v-col>
            </v-row>
          
            <v-btn large color="primary" :disabled="loading" @click="mutate()">Update Person</v-btn>
            <p v-if="error">An error occurred: {{ error }}</p>
          </v-container>
        </v-form>
      </template>
    </ApolloMutation>



<!-- DELETE PERSON -->
    <ApolloMutation
      :mutation="require('../graphql/RemovePerson.gql')"
      :variables="{
        id,
        name,
        age
        }"
        @done="onDone"
    >
      <template v-slot="{ mutate, loading, error }">
        
        <!-- Form here -->
        <v-form>
          <v-container>
            <v-card-title>Delete a Person</v-card-title>
            <v-row>
              <v-col cols="12" md="12">
                <v-text-field v-model="id" label="id" required filled></v-text-field>
              </v-col>
            </v-row>
          
            <v-btn large color="primary" :disabled="loading" @click="mutate()">Delete Person</v-btn>
            <p v-if="error">An error occurred: {{ error }}</p>
          </v-container>
        </v-form>
      </template>
    </ApolloMutation>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      id: '',
      name: '',
      age: '',
    }
  },
  methods: {
    onDone() {
      return console.log('Done')
    }
  }
}
</script>