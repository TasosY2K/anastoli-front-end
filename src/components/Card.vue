<template>
  <div class="card">
    <div class="centered">
      <h3>{{ info.name }}</h3>
    </div>
    <p>Περιοχή: {{ info.region }}</p>
    <p>Διεύθηνση: <a class="link" target="_blank" :href="'http://maps.google.com/?q=' + info.address + ', ' + info.region">{{ info.address }}</a></p>
    <p>Κλειστά μέχρι: {{ info.closed_until }}</p>
    <p class="underline">Σχόλια</p>
    <div class="centered">
      <div class="comments">
        <p v-if="info.comments">{{ info.comments }}</p>
        <p v-else>Δεν υπάρχουν σχόλια</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Card',
  props: {
    info: Object
  }
}
</script>

<style scoped>
.card {
  padding: 1rem;
  text-align: left;
  color: #e9e9e9;
  background-color: #292929;
  border-radius: 8px;
  transition-duration: 0.3s;
}

.card:hover {
  transform: translateY(-2px);
  -webkit-box-shadow: 0px 10px 27px -2px rgba(0,0,0,0.75);
  -moz-box-shadow: 0px 10px 27px -2px rgba(0,0,0,0.75);
  box-shadow: 0px 10px 27px -2px rgba(0,0,0,0.75);
}

.centered {
  text-align: center;
}

.centered h3 {
  margin-top: 0;
  font-weight: 800;
  margin-bottom: 1.6rem;
}

.link {
  text-decoration: none;
  color: #FF2950;
  padding: 2px;
  border-radius: 8px;
  transition-duration: 0.3s;
}

.link:hover {
  color: #eeeeee;
  background-color: #FF2950;
}

.underline {
  text-decoration: underline;
}

.comments {
  padding: 0.2rem;
  background-color: #111111;
  border-radius: 8px;
}
</style>
