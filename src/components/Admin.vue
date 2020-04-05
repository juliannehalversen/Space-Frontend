<template>
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
        <v-row>
          <v-col cols="12" md="12">
            <v-text-field v-model="name" label="name" required filled></v-text-field>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="12" md="12">
            <v-textarea v-model="age" label="age" type="number" rows="4" filled clearable></v-textarea>
          </v-col>
        </v-row>
       
        <v-btn large color="primary" :disabled="loading" @click="mutate()">Add Person</v-btn>
        <p v-if="error">An error occurred: {{ error }}</p>
      </v-container>
    </v-form>
  </template>
  </ApolloMutation>
</template>

<script>
export default {
  data: function() {
    return {
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