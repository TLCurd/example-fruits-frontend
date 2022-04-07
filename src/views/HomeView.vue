<script>
import axios from "axios";
// import { response } from "express";
export default {
  data: function () {
    return {
      message: "Check out these fruits!",
      fruits: [],
      newFruit: {
        name: "",
        color: "",
        description: "",
        image: ""
      },
      currentFruit: {}
    };
  },
  created: function () {
    console.log('in create');
    this.fruitsIndex();
  },
  methods: {
    fruitsIndex: function () {
      console.log('in fruits...');
      axios.get(`/fruits.json`).then(response => {
        console.log(response.data);
        this.fruits = response.data;
      });
    },
    createFruit: function () {
      console.log('creating fruits...');
      axios.post(`http://localhost:3000/fruits.json`, this.newFruit).then(response => {
        console.log(response.data);
        this.fruits.push(response.data);
      })
    },
    showFruit: function (theFruit) {
      console.log(theFruit);
      document.querySelector("#fruit-details").showModal();
      this.currentFruit = theFruit;
    }
  }
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
      <br />
      <img v-bind:src="fruit.image" />
      <br />
      <button v-on:click="showFruit(theFruit)">Let's get fruity</button>
      <hr />
    </div>
    <br />
    <p>
      Name:
      <input type="text" v-model="newFruit.name" />
    </p>
    <p>
      Color:
      <input type="text" v-model="newFruit.color" />
    </p>
    <p>
      Description:
      <input type="text" v-model="newFruit.description" />
    </p>
    <p>
      Image:
      <input type="text" v-model="newFruit.image" />
    </p>
    <button v-on:click="createFruit()">Add a new fruit!</button>

    <dialog id="fruit-details">
      <form method="dialog">
        <h1>Fruit info</h1>
        <p>
          Name:
          <input type="text" v-model="currentFruit.name" />
        </p>
        <p>
          Color:
          <input type="text" v-model="currentFruit.color" />
        </p>
        <p>
          Description:
          <input type="text" v-model="currentFruit.description" />
        </p>
        <p>
          Image:
          <input type="text" v-model="currentFruit.image" />
        </p>
        <button>Close</button>
      </form>
    </dialog>
  </div>
</template>

<style>
img {
  width: 300px;
}
</style>