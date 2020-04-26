<template>
  <v-app>
    <v-app-bar
      app
      color="#AA00CC"
      dark
    >
    
    <router-link to="/" class="white--text">GraphQL HOME</router-link>
    <router-link to="/admin" class="white--text">GraphQL CRUD</router-link>
    <router-link to="/resthome" class="white--text">REST Home</router-link>
    </v-app-bar>

    <v-content>
      <!-- <div>
        <router-link to="/">GraphQL HOME</router-link> |
        <router-link to="/admin">GraphQL CRUD</router-link>
        <router-link to="/resthome">REST Home</router-link>
      </div> -->

      <router-view/>
    </v-content>
  </v-app>
</template>

<script>
//import ApolloExample from './components/ApolloExample';
//import CourseCard from './components/CourseCard'
//import Admin from './components/Admin'

export default {
  name: 'App',

  components: {
    //ApolloExample,
    //CourseCard,
    //Admin
  },

  data: () => ({
    //
  }),
};
</script>


<style scoped>
a {
  text-decoration: none;
  margin-left: 10px;
  margin-right: 10px;
  color: white;
  font-weight: 500;
  font-size: 18px;
}
a:hover {
  color: pink;
}
/* * {
  background-image: url('./assets/stars2.jpg');
} */
</style>