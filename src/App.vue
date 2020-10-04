<template>
  <div>
    <p id="header">Σχολεία Κλειστά Λόγω Του Covid-19</p>
    <p id="credits">designed by <a href="https://github.com/pasenidis">ed</a> & <a href="https://github.com/TasosY2K" target="_blank">tasos</a></p>
    <input type="text" id="search-box" placeholder="Αναζήτησε σχολεία" v-model="searchString" @input="this.searchSchool">
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
  methods: {
    searchSchool() {
      if (this.searchString) {
        let schoolResults = []
        for (let i = 0; i < this.schoolDataOrigin.length; i++) {
          if (this.schoolDataOrigin[i].name.includes(this.searchString)) {
            schoolResults.push(this.schoolDataOrigin[i])
          }
        }
        this.schoolData = schoolResults
      } else {
        axios.get(`http://fuck.plasmasearch.cf`).then(response => this.schoolData = response.data.schools);  
      }
    }
  },
  data () {
    return {
      searchString: null,
      schoolDataOrigin: null,
      schoolData: null
    }
  },
  mounted () {
    axios.get(`http://fuck.plasmasearch.cf`).then(response => {
      this.schoolData = response.data.schools
      this.schoolDataOrigin = response.data.schools
    });  
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

#search-box {
  width: 17em;
  font-size: 1.1em;
  font-family: 'Comfortaa', cursive;
  padding: 0.6em;
  background-color: #292929;
  border-radius: 8px;
  transition-duration: 0.3s;
  border: none;
  margin-bottom: 1rem;
  color: #e9e9e9;
}

#search-box:focus {
  outline: none;
}

#search-box:hover {
  transform: translateY(-1px);
  -webkit-box-shadow: 0px 7px 15px -2px rgba(0,0,0,0.75);
  -moz-box-shadow: 0px 7px 15px -2px rgba(0,0,0,0.75);
  box-shadow: 0px 7px 15px -2px rgba(0,0,0,0.75);
}
</style>
