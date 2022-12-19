<template>
  <form @submit.prevent="submitForm">
    <label for="name">Name:</label>
    <input type="text" v-model="recipe.name" id="name" />
    <br />
    <label for="ingredients">Ingredients:</label>
    <textarea v-model="recipe.ingredients" id="ingredients"></textarea>
    <br />
    <label for="steps">Steps:</label>
    <textarea v-model="recipe.steps" id="steps"></textarea>
    <br />
    <label for="rating">Rating:</label>
    <input type="number" v-model="recipe.rating" id="rating" min="1" max="5" />
    <br />
    <label for="favorite">Favorite:</label>
    <input type="checkbox" v-model="recipe.favorite" id="favorite" />
    <br />
    <button type="submit">Submit</button>
    <button type="reset" @click="resetForm">Reset</button>
  </form>
  <button @click="deleteRecipe">Delete</button>
  <button @click="updateRecipe">Update</button>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      recipe: {
        name: '',
        ingredients: '',
        steps: '',
        rating: '',
        favorite: false,
      },
    };
  },
  methods: {
    async submitForm() {
      try {
        const response = await axios.post('/', this.recipe);
        console.log(response.data);
      } catch (error) {
        console.error(error);
      }
    },
    resetForm() {
      this.recipe = {
        name: '',
        ingredients: '',
        steps: '',
        rating: '',
        favorite: false,
      };
    },
    async deleteRecipe() {
      try {
        const response = await axios.delete(`/${this.recipe.id}`);
        console.log(response.data);
      } catch (error) {
        console.error(error);
      }
    },
    async updateRecipe() {
      try {
        const response = await axios.put(`/${this.recipe.id}`, this.recipe);
        console.log(response.data);
      } catch (error) {
        console.error(error);
      }
    },
  },
};
</script>