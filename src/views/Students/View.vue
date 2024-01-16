<template>
  <div class="container">
    <div class="card">
      <div class="card-header">
        <h4>
          Students
          <RouterLink to="/student/create" class="btn btn-primary float-end"
            >Add Student</RouterLink
          >
        </h4>
      </div>
      <div class="card-body">
        <table class="table table-bordered">
          <thead>
            <tr>
              <th>ID</th>
              <th>Profile</th>
              <th>Name</th>
              <th>Email</th>
              <th>Action</th>
            </tr>
          </thead>
          <tbody v-if="this.students.length > 0">
            <tr v-for="(student, index) in this.students" :key="index">
              <td>{{ student.id }}</td>
              <td>
                <img
                  :src="student.avatar"
                  class="rounded float-left"
                  alt="{{ student.first_name + ' ' + student.last_name }}"
                />
              </td>
              <td>{{ student.first_name + " " + student.last_name }}</td>
              <td>{{ student.email }}</td>
              <td>
                <RouterLink type class="btn btn-warning float-end" to="/"
                  >Edit</RouterLink
                >
                <button type="button" class="btn btn-danger float-end" to="/">
                  Delete
                </button>
              </td>
            </tr>
          </tbody>
          <tbody v-else>
            <tr>
              <td colspan="5">No data found!</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { RouterLink } from "vue-router";

export default {
  name: "students",
  data() {
    return {
      students: [],
    };
  },
  mounted() {
    // console.log("Test");
    this.getStudents();
  },
  methods: {
    getStudents() {
      axios.get("https://reqres.in/api/users").then((res) => {
        this.students = res.data.data;
        console.log(res.data.data);
      });
    },
  },
  components: { RouterLink },
};
</script>
