<template>
  <div>
    <h1>Planets</h1>
    <PlanetsList />
  </div>
</template>

<script>
import PlanetsList from './components/PlanetsList.vue'
import 'bootstrap/dist/css/bootstrap.min.css';

export default {
  name: 'App',
  components: {
    PlanetsList
  }
}
</script>
