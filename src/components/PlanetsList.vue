<template>
    <div>
      <ul>
        <li v-for="planet in planets" :key="planet.name">{{ planet.name }}</li>
      </ul>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        planets: []
      };
    },
    mounted() {
      axios.get('https://swapi.dev/api/planets/')
        .then(response => {
          this.planets = response.data.results;
        });
    }
  };
  </script>
  