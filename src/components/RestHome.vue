<template>
<div>
    
     <v-row>
         <v-container>
        <v-col cols="12">
            
            <h1>RESTFUL API Home</h1>
            <v-btn @click="getData" class="dataBtn" id="getDataBtn">Get Data</v-btn>
        </v-col>
        <div> 
        <v-row>
          <v-col cols="3" v-for="(item, i) in people" :key="i">
            <v-card class="mx-auto" max-width="350">
              <v-card-text>
                <p class="name">
                  {{ item._id }}
                </p>
                <p>{{ item.title }}</p>
                <p>{{ item.price }}</p>
                <p>{{ item.description }}</p>
                <p>{{ item.imageURL }}</p>
              </v-card-text>
            </v-card>
          </v-col>
        </v-row>
      </div>
         </v-container>
     </v-row>


      <v-row>
        <v-col cols="12">
        <v-form>
            <v-container>
                <v-card-title>Get a Person</v-card-title>
                <!-- <v-row>
                    <v-col cols="6" md="6">
                        <v-text-field v-model="id" label="ID" type="number" rows="4" required filled></v-text-field>
                    </v-col>
                </v-row>   -->      
                <v-btn large color="primary" @click="getOnePerson()">Get One Person</v-btn>
            </v-container>
      </v-form>
        </v-col>
     </v-row>
     <div> 
        <v-row>
          <v-col cols="3">
            <v-card class="mx-auto" max-width="350">
              <v-card-text>
                <p class="name">{{ person._id }}</p>
                <p>{{ person.title }}</p>
                <p>{{ person.price }}</p>
                <p>{{ person.description }}</p>
                <p>{{ person.imageURL }}</p>
              </v-card-text>
            </v-card>
          </v-col>
        </v-row>
      </div>





   <!--    <v-row>
        <v-col cols="12">
        <v-form>
            <v-container>
                <v-card-title>Create a Person</v-card-title>
                <v-row>
                    <v-col cols="6" md="6">
                        <v-text-field v-model="id" label="ID" type="number" rows="4" required filled></v-text-field>
                    </v-col>
                </v-row>   
                <v-btn large color="primary" @click="createPerson()">Get One Person</v-btn>
            </v-container>
      </v-form>
        </v-col>
     </v-row> -->
     <v-btn large color="primary" @click="createPerson()">Create Person</v-btn>


</div>
</template>

<script>
import axios from "axios";

export default {
    data: () => ({
        people: [],
        person: []
  }),

    methods: {
      // GET ALL PEOPLE
      getData() {
      return axios
        .get("http://localhost:3000/admin/getAllProducts")
        .then(response => {
        console.log(response);
        this.people = response.data;
        console.log(this.people);
        })
        .catch(error => console.log(error));
      },


      // GET ONE PERSON
      getOnePerson() {
        return axios
        .get('http://localhost:3000/admin/single-product', {"productId": "5e4d87b7fec85ddb8c463451"})
        .then(response => {
            console.log(response)
            this.person = response.data;
            console.log(this.person);
        }).catch(error => console.log(error));
    },


    // CREATE PERSON
    createPerson() {
      fetch('http://localhost:3000/admin/add-product', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({
          title: 'test',
          price: 45,
          description: 'test create',
          imageURL: 'https://www.syfy.com/sites/syfy/files/styles/1200x680/public/wire/legacy/LukeLightsaber.jpg'
        })
      })
      .then(response => {
        console.log(response);
      })
      .catch(error => {
        console.log(error);
      })
     /*  axios({
      method: 'post',
      url: 'http://localhost:3000/admin/add-product',
      data: {
        "title": "test",
        "price": 45,
        "description": "test create",
        "imageUrl": "https://www.syfy.com/sites/syfy/files/styles/1200x680/public/wire/legacy/LukeLightsaber.jpg"
      },
      headers: {'Content-Type': 'application/json' }
      })
      .then(response => {
          //handle success
          console.log(response);
      })
      .catch(response => {
          //handle error
          console.log(response); 
      });*/

    }
  }
};

</script>

<style scoped>

</style>