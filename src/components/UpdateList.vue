<template>
  <div class="container">
    <h1>Update using axios PUT</h1>

    <table class="book-table">
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

        <td>
          <button class="edit-btn" @click="editItem(item)">
            Edit
          </button>
        </td>
      </tr>
    </table>

    <!-- Edit Section -->
    <div class="edit-box" v-if="editData.id">
      <h3>Edit Employee</h3>

      <input v-model="editData.empid" placeholder="Emp ID" />
      <input v-model="editData.name" placeholder="Name" />
      <input v-model="editData.department" placeholder="Department" />
      <input v-model="editData.salary" placeholder="Salary" />
      <input v-model="editData.designation" placeholder="Designation" />

      <button class="update-btn" @click="updateData">
        Update
      </button>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "UpdateList",

  data() {
    return {
      list: [],
      editData: {
        id: null,
        empid: "",
        name: "",
        department: "",
        salary: "",
        designation: ""
      }
    };
  },

  methods: {
    async fetchData() {
      try {
        const resp = await axios.get(
          "https://69e7505568208c1debe8a8c4.mockapi.io/api/employee"
        );
        this.list = resp.data;
      } catch (err) {
        console.error(err);
      }
    },

    editItem(item) {
      this.editData = { ...item };
    },

    async updateData() {
      try {
        await axios.put(
          `https://69e7505568208c1debe8a8c4.mockapi.io/api/employee/${this.editData.id}`,
          this.editData
        );

        this.fetchData();

        this.editData = {
          id: null,
          empid: "",
          name: "",
          department: "",
          salary: "",
          designation: ""
        };

        alert("Employee updated successfully");
      } catch (err) {
        console.error(err);
        alert("Update failed");
      }
    }
  },

  mounted() {
    this.fetchData();
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

.book-table {
  width: 100%;
  border-collapse: collapse;
}

.book-table th {
  background: #3498db;
  color: white;
  padding: 10px;
}

.book-table td {
  padding: 8px;
  border-bottom: 1px solid #ddd;
}

.edit-btn {
  background: orange;
  color: white;
  border: none;
  padding: 6px 12px;
  cursor: pointer;
}

.update-btn {
  background: green;
  color: white;
  border: none;
  padding: 8px 16px;
  cursor: pointer;
}

.edit-box {
  margin-top: 20px;
}
</style>