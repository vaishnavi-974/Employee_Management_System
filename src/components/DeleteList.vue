<template>
  <div class="container">
    <h1>Delete using axios delete</h1>

    <table border="1" width="80%" align="center">
      <tr>
        <th>empid</th>
        <th>name</th>
        <th>department</th>
        <th>salary</th>
        <th>designation</th>
        <th>action</th>
      </tr>

      <tr v-for="item in list" :key="item.id">
        <td>{{ item.empid }}</td>
        <td>{{ item.name }}</td>
        <td>{{ item.department }}</td>
        <td>{{ item.salary }}</td>
        <td>{{ item.designation }}</td>

        <td>
  <button 
    class="btn btn-danger btn-sm"
    @click="deleteData(item.id)"
  >
    Delete
  </button>
</td>
      </tr>
    </table>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "DeleteList",

  data() {
    return {
      list: []
    };
  },

  methods: {
    async fetchData() {
      try {
        const response = await axios.get(
          "https://69e7505568208c1debe8a8c4.mockapi.io/api/employee"
        );

        this.list = response.data;
      } catch (error) {
        console.log(error);
      }
    },

    async deleteData(id) {
      try {
        await axios.delete(
          `https://69e7505568208c1debe8a8c4.mockapi.io/api/employee/${id}`
        );

        alert("Deleted successfully");

        this.fetchData();
      } catch (error) {
        console.log(error);
      }
    }
  },

  mounted() {
    this.fetchData();
  }
};
</script>