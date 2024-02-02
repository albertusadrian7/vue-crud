<template>
  <div class="container mt-5">
    <div class="card">
      <div class="card-header">
        <h4>Add Student</h4>
      </div>
      <div class="card-body">
        <div class="mb-3">
          <label for="">Name</label>
          <input v-model="model.student.product_name" type="text" class="form-control" />
        </div>
        <div class="mb-3">
          <label for="">Desc</label>
          <input v-model="model.student.description" type="text" class="form-control" />
        </div>
        <div class="mb-3">
          <button type="button" @click="saveStudent" class="btn btn-primary">
            Submit
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "studentCreate",
  data() {
    return {
      model: {
        student: {
          product_name: "",
          description: "",
        },
      },
    };
  },
  methods: {
    saveStudent() {
      axios
        .post("http://localhost:8080/api/product", this.model.student)
        .then((result) => {
          console.log(result.data);
          // alert(result.data);
          this.model.student = {
            product_name: "",
            description: "",
          };
        })
        .catch(function (error) {
          console.log(error);
        });
    },
  },
};
</script>
