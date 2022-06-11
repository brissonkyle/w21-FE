<template>
  <div class="hello">
    <input v-model="animalName" type="text" id='animalInput'>
    <input v-model="imageUrl" type="text" id='imageInput'>
    <button @click="postAnimal">POST</button>
    <button @click="getAnimals">GET</button>
    <div v-for="animal in animalArr" :key="animal.animalId">
      {{ animal.animalId }}
      <h1>{{ animal.name }}</h1>
      <img :src="animal.imageUrl">
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'HelloWorld',
  data() {
    return {
      animalName: null,
      imageUrl : null
    }
  },
  methods: {
    getAnimals() {
      console.log('RUNNING GET');
      axios.request({
        method : "GET",
        url : 'http://127.0.0.1:5000/api/animals'
      }).then((response)=> {
        console.log(response);
        this.animalArr = response.data;
      }).catch(()=> {
        
      })
    },
    postAnimal() {
      console.log('RUNNING POST');
      axios.request({
        method : "POST",
        url : 'http://127.0.0.1:5000/api/animals',

        data() {
          return {
            animalName: this.animalName,
            imageUrl : this.imageUrl
          }
        },
      }).then((response)=> {
        console.log(response);
        this.getAnimals
      }).catch((error)=> {
        console.log(error);
      })
    },
    mounted () {
      this.getAnimals();
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
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
