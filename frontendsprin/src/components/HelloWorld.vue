<template>
  <div class="hello">
    <h1>Seleccion de Ciudades</h1>
    <form @submit.prevent="" class="create-task-form">
    <select id="label" v-model="Country.id">
      <option value="" disabled selected>Selecciona un Pais</option>
      <option v-for="country in countries">{{ country.name }}</option>
    </select>
    </form>
  </div>
</template>
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
<script>
import axios from 'axios';

export default {
  data() {
    return {
      Country: {
        id:'',
        name: '',
      },
      countries: [],
    };
  },
  methods: {
    loadLabels() {
      axios.get(`http://localhost:8080/api/v1/country/`)
          .then(response => {
            this.countries = response.data;
            console.log('Etiquetas cargadas:', this.countries);
          })
          .catch(error => {
            console.error('Error al obtener las etiquetas:', error);
          });
    },
  },
  mounted() {
    this.loadLabels();
  },
};
</script>