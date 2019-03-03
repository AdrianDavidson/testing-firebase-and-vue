<template>
  <div class="hello">
    <div>
  <article v-for="(Receipt, idx) in Receipts" :key="idx">
    <img :src="Receipt.image">
    <h1>{{ Receipt.name }}</h1>
  </article>
</div>
<form @submit="addLocation(name, image)">
    <input v-model="name" placeholder="Location Name">
    <input v-model="image" placeholder="Location Image URL">
    <button type="submit">Add New Location</button>
</form>
  </div>
  
</template>

<script>
import { db } from '../main'
export default {
  name: 'HelloWorld',
  data () {
    return {
      Receipts: [],
      name: '',      
      image: ''      
    }
  },
  firestore () {
    return {
      Receipts: db.collection('Receipts').orderBy('createdAt')
    }
  },
  methods: { 
    addLocation (name, image) {
      const createdAt = new Date()
      db.collection('Receipts').add({ name, image, createdAt })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
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
