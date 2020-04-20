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
     <v-card-title>Create a Person</v-card-title>
     <v-btn large color="primary" @click="createPerson()">Create Person</v-btn>

     <v-card-title>Update a Person</v-card-title>
     <v-btn large color="primary" @click="updatePerson()">Update Person</v-btn>

     <v-card-title>Delete a Person</v-card-title>
     <v-btn large color="primary" @click="deletePerson()">Delete Person</v-btn>


</div>
</template>

<script>
import axios from "axios";

export default {
    data: () => ({
        people: [],
        person: [],
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
        const personId = `5e4d87b7fec85ddb8c463451`;
        const url = `http://localhost:3000/admin/single-product/` + personId;
        return axios
        .get(url)
        .then(response => {
            console.log(response)
            this.person = response.data;
            console.log(this.person);
        }).catch(error => console.log(error));
    },


    // CREATE PERSON
    createPerson() {
        const url = `http://localhost:3000/admin/add-product`;
        const data = { 
          title: 'test', 
          price: 45, 
          description: 'test create', 
          imageUrl: 'https://www.syfy.com/sites/syfy/files/styles/1200x680/public/wire/legacy/LukeLightsaber.jpg' 
        };
        return axios
        .post(url, data)
        .then(response => {
            console.log(response)
            this.person = response.data;
            console.log(this.person);
        }).catch(error => console.log(error));
    },


    // UPDATE PERSON 
    updatePerson() {
      const url = `http://localhost:3000/admin/edit-product`;
      const data = { 
          productId: '5e4d87b7fec85ddb8c463451',
          title: 'Luke Sky',
          price: '50',
          description: 'I find your lack of faith disturbing.',
          imageUrl: 'test image'
        };
      return axios
      .post(url, data)
      .then(response => {
          alert(response.data);
      }).catch(error => console.log(error));
    },


    // DELETE PERSON 
    deletePerson() {
      const url = `http://localhost:3000/admin/delete-product`;
      const data = { 
          productId: '5e9dd4e513b25d527d8bc303'
        };
      return axios
      .post(url, data)
      .then(response => {
          alert(response.data);
      }).catch(error => console.log(error));
    }

  }
};

</script>

<style scoped>

</style>