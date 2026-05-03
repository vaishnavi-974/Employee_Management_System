<template>
  <div>
    <h1>Create using Axios POST</h1>

    <form @submit.prevent="postData">
      emp_id:
      <input type="number" v-model="posts.empid" placeholder="id" />
      <br /><br />

      ename:
      <input type="text" v-model="posts.name" placeholder="ename" />
      <br /><br />

      dept:
      <input type="text" v-model="posts.department" placeholder="dept" />
      <br /><br />

      sal:
      <input type="number" v-model="posts.salary" placeholder="sal" />
      <br /><br />

      designation:
      <input type="text" v-model="posts.designation" placeholder="designation" />
      <br /><br />

      <button type="submit">Post</button>
    </form>

    <p v-if="successMessage" style="color: green;">
      {{ successMessage }}
    </p>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "PostComp",
  data() {
    return {
      posts: {
        empid: "",
        name: "",
        department: "",
        salary: "",
        designation: ""
      },
      successMessage: ""
    };
  },

  methods: {
    async postData() {
      try {
        const res = await axios.post(
          "https://69e7505568208c1debe8a8c4.mockapi.io/api/employee",
          this.posts
        );

        console.log("Response:", res.data);

        this.successMessage = "Data posted successfully!";
        // reset form
        this.posts = {
          empid: "",
          name: "",
          department: "",
          salary: "",
          designation: ""
        };
      } catch (err) {
        console.log("Error:", err.response || err);
        this.successMessage = "Failed to post data!";
      }
    }
  }
};
</script>