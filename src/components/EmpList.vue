<template>
  <div class="container">
    <h1>Read using Axios GET</h1>

    <table class="emp-table">
      <tr>
        <th>empid</th>
        <th>name</th>
        <th>department</th>
        <th>salary</th>
        <th>designation</th>
      </tr>

      <tr v-for="item in list" :key="item.id">
        <td>{{ item.empid }}</td>
        <td>{{ item.name }}</td>
        <td>{{ item.department }}</td>
        <td>{{ item.salary }}</td>
        <td>{{ item.designation }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "EmpList",

  data() {
    return {
      list: []
    };
  },

  mounted() {
    axios
      .get("https://69e7505568208c1debe8a8c4.mockapi.io/api/employee")
      .then((resp) => {
        this.list = resp.data;
      })
      .catch((err) => {
        console.error(err);
      });
  }
};
</script>

<style scoped>
.container {
  width: 70%;
  margin: 40px auto;
  text-align: center;
  font-family: Arial, sans-serif;
}

h1 {
  margin-bottom: 20px;
  color: #2c3e50;
}

.emp-table {
  width: 100%;
  border-collapse: collapse;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.emp-table th {
  background-color: #3498db;
  color: white;
  padding: 10px;
}

.emp-table td {
  padding: 10px;
  border-bottom: 1px solid #ddd;
}

.emp-table tr:nth-child(even) {
  background-color: #f9f9f9;
}

.emp-table tr:hover {
  background-color: #f1f1f1;
}
</style>