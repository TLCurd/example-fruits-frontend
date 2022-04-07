<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Check out these fruits!",
      fruits: [],
      newFruitParams: {}
    };
  },
  created: function () {
    console.log('in create');
    this.fruitsIndex();
  },
  methods: {
    fruitsIndex: function () {
      console.log('in fruits...');
      axios.get(`http://localhost:3000/fruits.json`).then(response => {
        console.log(response.data);
        this.fruits = response.data;
      });
    },
    createFruit: function () {
      console.log('creating fruits...');
      axios.post(`http://localhost:3000/fruits.json`)
    }
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <hr />
    <br />

    <div v-for="fruit in fruits">
      {{ fruit.id }}.
      <b>{{ fruit.name }}</b>
      <br />
      <img v-bind:src="fruit.image" />
      <hr />
    </div>
    <br />
    <p>
      Name:
      <input v-model="newFruitParams.name" />
    </p>
    <p>
      Color:
      <input v-model="newFruitParams.color" />
    </p>
    <p>
      Description:
      <input v-model="newFruitParams.description" />
    </p>
    <p>
      Image:
      <input v-model="newFruitParams.image" />
    </p>
    <button v-on:click="createFruit()">Add a new fruit!</button>

    <button v-on:click="showProduct()">Let's get fruity</button>
  </div>
</template>

<style>
img {
  width: 300px;
}
</style>