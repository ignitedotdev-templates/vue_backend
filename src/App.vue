<template>
  <div class="container">
    <h1>Hello People</h1>
    <table v-if="data">
      <thead>
      <tr>
        <th>ID</th>
        <th>Name</th>
        <th>Email</th>
        <th>Age</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="data in data">
        <td>{{ data.id }}</td>
        <td>{{ data.name }}</td>
        <td>{{ data.email }}</td>
        <td>{{ data.age }}</td>
      </tr>
      </tbody>
    </table>
    <p v-if="error" class="error">Error: {{ error.message }}</p>
  </div>
</template>

<script setup lang="ts">
import axios from 'axios';
import { ref, onMounted } from 'vue';

// Define the API endpoint
const apiUrl = 'https://svc-app-nodejs-1724001248.web.onignite.dev/users';

// Define reactive variables to hold the data and error
const data = ref<any>(null);
const error = ref<any>(null);

const fetchData = async () => {
  try {
    const response = await axios.get(apiUrl);
    // Handle success
    data.value = response.data;
  } catch (err) {
    // Handle error
    error.value = err;
  }
};

// Fetch data when the component is mounted
onMounted(fetchData);
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  margin: 20px;
}

table {
  width: 80%;
  border-collapse: collapse;
  margin-top: 20px;
}

th, td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: center;
}

th {
  background-color: #f4f4f4;
}

.error {
  color: red;
  margin-top: 20px;
}
</style>
