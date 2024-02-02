<script>
import axios from "axios";
import { RouterLink } from "vue-router";

let students = [];
let model = {
  student: {
    product_name: "",
    description: "",
  }
}

export default {
  name: "students",
  data() {
    return {
      id: "",
      students: [],
      model: {
        student: {
          product_name: "",
          description: "",
        }
      },
      isModalVisible: true
    };
  },
  mounted() {
    // console.log("Test");
    this.getStudents();
  },
  methods: {
    getStudents() {
      axios.get("http://localhost:8080/api/products").then((res) => {
        this.students = res.data.products;
        // console.log(res.data.products);
      });
    },
    getStudent(id) {
      this.showModal();
      axios.get("http://localhost:8080/api/product/" + id).then((res) => {
        this.model.student = res.data.product;
        this.id = id;
        // console.log("ID" + this.id);
        // console.log(res.data.product);
      });
    },
    updateStudent(id) {
      axios
        .put("http://localhost:8080/api/product/" + this.id, this.model.student)
        .then((result) => {
          console.log(result.data);
          this.model.student = {
            product_name: "",
            description: "",
          };
          this.id = "";
        })
        .catch(function (error) {
          console.log(error);
        });
      $("#formModal").modal("hide");
    },
    showModal() {
      this.isModalVisible = true;
    },
    closeModal() {
      this.isModalVisible = false;
    }
  },
  components: { RouterLink },
};
</script>


<template>
  <div class="container">
    <div class="card">
      <div class="card-header">
        <h4>
          Students
          <RouterLink to="/student/create" class="btn btn-primary float-end">Add Student</RouterLink>
        </h4>
      </div>
      <div class="card-body">
        <table class="table table-bordered">
          <thead>
            <tr>
              <th>ID</th>
              <th>Name</th>
              <th>Price</th>
              <th>Action</th>
            </tr>
          </thead>
          <tbody v-if="this.students.length > 0">
            <tr v-for="(student, index) in this.students" :key="index">
              <td>{{ student.id }}</td>
              <!-- <td>
                <img
                  :src="student.avatar"
                  class="rounded float-left"
                  alt="{{ student.first_name + ' ' + student.last_name }}"
                />
              </td> -->
              <td>{{ student.product_name }}</td>
              <td>{{ student.description }}</td>
              <td>
                <button @click="showModal" type="button" class="btn btn-primary float-end">
                  Edit
                </button>
                <button type="button" class="btn btn-danger float-end">
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

  <FormModal></FormModal>
</template>

