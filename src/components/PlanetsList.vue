<template>
  <div class="container mt-3">
    <h2>Star Wars Planets</h2>

    <div v-if="loading">
      Loading planets...
    </div>

    <div v-else>
      <div class="mb-3">
        <label for="sort-select" class="form-label">Sort by:</label>
        <select id="sort-select" class="form-select" v-model="sortKey" @change="sortPlanets">
          <option value="name">Name</option>
          <option value="population">Population</option>
          <option value="diameter">Diameter</option>
        </select>
      </div>

      <ul class="list-group">
        <li v-for="planet in planets" :key="planet.name" class="list-group-item">
          {{ planet.name }} - Population: {{ planet.population }}, Diameter: {{ planet.diameter }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      planets: [],
      loading: false,
      sortKey: 'name',
    };
  },
  mounted() {
    this.fetchPlanets();
  },
  methods: {
    fetchPlanets() {
      this.loading = true;
      axios.get('https://swapi.dev/api/planets/')
        .then(response => {
          this.planets = response.data.results;
          this.sortPlanets();
        })
        .catch(error => {
          console.error("Error fetching planets:", error);
        })
        .finally(() => {
          this.loading = false;
        });
    },
    sortPlanets() {
      this.planets.sort((a, b) => {
        if (this.sortKey === 'population' || this.sortKey === 'diameter') {
          return parseInt(a[this.sortKey]) - parseInt(b[this.sortKey]);
        }
        return a[this.sortKey].localeCompare(b[this.sortKey]);
      });
    }
  }
};
</script>
  