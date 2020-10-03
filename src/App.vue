<template>
  <div>
    <p id="header">Σχολεία Κλειστά Λόγω Του Covid-19</p>
    <p id="credits">designed by <a href="https://github.com/pasenidis">ed</a> & <a href="https://github.com/TasosY2K" target="_blank">tasos</a></p>
    <div id="card-container">
      <div v-for="i in schoolData" :key="i">
        <Card :info="i"/>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Card from './components/Card.vue'

export default {
  name: 'App',
  components: {
    Card
  },
  data () {
    return {
      schoolData: null
    }
  },
  mounted () {
    axios.get('http://fuck.plasmasearch.cf').then(response => (this.schoolData = response.data.schools))
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Comfortaa:wght@600&display=swap');

#app {
  font-family: 'Comfortaa', cursive;
  text-align: center;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  padding: 0.5rem;
}

#header {
  font-size: 2em;
}

#credits a {
  text-decoration: none;
  color: #FF2950;
}

#credits a:hover {
  text-decoration: underline;
}

#card-container {
  max-width: 1200px;
  margin: 0 auto;
  display: grid;
  grid-gap: 1rem;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
}
</style>
