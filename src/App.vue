<template>
  <div>

    <!-- Navbar -->
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark px-4">
      <a class="navbar-brand text-white" href="#">Employee Manager</a>

      <div class="collapse navbar-collapse justify-content-end">
        <ul class="navbar-nav">
          <li class="nav-item">
            <a class="nav-link" @click="view='home'">Home</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" @click="view='post'">Post Data</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" @click="view='get'">Get Data</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" @click="view='update'">Update Data</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" @click="view='delete'">Delete Data</a>
          </li>
        </ul>
      </div>
    </nav>

    <!-- HOME PAGE -->
<div v-if="view==='home'" class="container mt-5">

  <div class="text-center mb-5">
    <h1 class="fw-bold text-dark">Employee Dashboard</h1>
    <p class="text-secondary">
      Manage employee records easily with simple CRUD operations
    </p>
  </div>

  <div class="row g-4">

    <!-- Add Employee -->
    <div class="col-md-3">
      <div class="card shadow h-100 text-center p-3">
        <h5 class="mb-3">Add Employee</h5>
        <p class="text-muted">Insert new employee details</p>
        <button class="btn btn-outline-primary" @click="view='post'">
          Add
        </button>
      </div>
    </div>

    <!-- View -->
    <div class="col-md-3">
      <div class="card shadow h-100 text-center p-3">
        <h5 class="mb-3">View Employees</h5>
        <p class="text-muted">See all employee records</p>
        <button class="btn btn-outline-success" @click="view='get'">
          View
        </button>
      </div>
    </div>

    <!-- Update -->
    <div class="col-md-3">
      <div class="card shadow h-100 text-center p-3">
        <h5 class="mb-3">Update Details</h5>
        <p class="text-muted">Modify employee information</p>
        <button class="btn btn-outline-warning" @click="view='update'">
          Update
        </button>
      </div>
    </div>

    <!-- Delete -->
    <div class="col-md-3">
      <div class="card shadow h-100 text-center p-3">
        <h5 class="mb-3">Delete Employee</h5>
        <p class="text-muted">Remove employee from system</p>
        <button class="btn btn-outline-danger" @click="view='delete'">
          Delete
        </button>
      </div>
    </div>

  </div>

</div>

    <!-- COMPONENT VIEWS -->
    <div class="container mt-4">

      <PostComp v-if="view==='post'" />
      <EmpList v-if="view==='get'" />
      <UpdateList v-if="view==='update'" />
      <DeleteList v-if="view==='delete'" />

    </div>

  </div>
</template>

<script>
import PostComp from "./components/PostComp.vue";
import EmpList from "./components/EmpList.vue";
import UpdateList from "./components/UpdateList.vue";
import DeleteList from "./components/DeleteList.vue";

export default {
  name: "App",
  components: {
    PostComp,
    EmpList,
    UpdateList,
    DeleteList
  },
  data() {
    return {
      view: "home"
    };
  }
};
</script>

<style>
.card:hover {
  transform: scale(1.05);
  transition: 0.3s;
}
body {
  background-color: #f8f9fa;
}
.nav-link {
  cursor: pointer;
}
</style>