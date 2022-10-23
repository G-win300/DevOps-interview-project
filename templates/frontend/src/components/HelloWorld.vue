<template>
    <v-container>
      <v-row class="text-center">
        <v-col cols="12">
          <v-img
            :src="require('../assets/devops44.png')"
            class="my-3"
            contain
            height="200"
          />
        </v-col>
  
        <v-col class="mb-4">
          <h1 class="display-2 font-weight-bold mb-3">
            I am Godwin Effiong, your Devops Engineer!
          </h1>
  
          <p class="subheading font-weight-regular">
            This simple app displays the current time which is <span>{{current_time}}</span>
          </p>
           <v-btn
              text
              color="primary"
              @click=" getTime();"
            >request time</v-btn>
  
        </v-col>
  
      </v-row>
    </v-container>
  </template>
  
  <script>
    import axios from 'axios';
    export default {
      name: 'HelloWorld',
      data: () => ({ 
        current_time : "placeholder"
      }),
      methods: {
        getTime: function() {
          axios
            // .get('http://localhost:9999/time')
            .get('http://kube.devopsapp.cloud:9999/time')
            .then(response => (this.current_time = response["data"]["current"]))
        }
      }
    }
  </script>