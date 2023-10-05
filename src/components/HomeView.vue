<script setup>
import foodData from "../data.json"
import { ref } from "vue"
import { useRouter } from "vue-router"

const router = useRouter()
const foods = ref(foodData)

// Define data properties for user input
const userInput = {
  name: '',
  price: ''
}

// Function to handle form submission
function handleSubmit() {
  // Do something with the user input data (e.g., add it to the 'foods' array)
  const newFood = {
    id: foods.length + 1, // Generate a new ID
    name: userInput.name,
    price: userInput.price
  }

  foods.value.push(newFood)

  // Clear the input fields
  userInput.name = ''
  userInput.price = ''
}
</script>

<template>
  <main class="container">
    <h1>Menu</h1>
    <div class="cards">
      <div v-for="food in foods" :key="food.id" class="card" @click="router.push(`/food/${food.id}`)">
        <h1>{{ food.name }}</h1>
        <p>{{ food.price }}</p>
      </div>
    </div>
    
    <!-- Add a form for user input -->
    <form @submit.prevent="handleSubmit" class="input-form">
      <label for="name">Add Pizza:</label>
      <input type="text" id="name" name="name" v-model="userInput.name" required>
      
      <label for="price">Price:</label>
      <input type="number" id="price" name="price" v-model="userInput.price" required>
      
      <button type="submit">Add Food</button>
    </form>
  </main>
</template>

<style scoped>
.container {
  max-width: 960px; /* Limit the maximum width of the container */
  margin: 0 auto; /* Center the container horizontally */
  padding: 20px;
  background-color: #f0f0f0;
}

.cards {
  display: flex;
  flex-wrap: wrap; /* Allow cards to wrap to the next line */
  margin-top: 20px; /* Increase top margin for spacing */
  justify-content: space-between; /* Distribute cards evenly with spacing */
}

.card {
  box-shadow: 1px 1px 10px rgba(0, 0, 0, 0.2);
  padding: 15px;
  width: calc(33.33% - 15px); /* Adjust card width to create a 3-column layout */
  margin-bottom: 20px;
  background-color: white;
  transition: background-color 0.3s;
}

.input-form {
  margin-top: 20px;
}

/* Add other CSS styles as needed */
</style>
