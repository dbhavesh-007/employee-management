<template>
  <div class="card p-3">
    <h4>Employee List</h4>

    <table class="table table-striped mt-3">
      <thead>
        <tr>
          <th>ID</th>
          <th>Name</th>
          <th>Designation</th>
          <th>Department</th>
          <th>Salary</th>
          <th>Actions</th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="emp in employees" :key="emp.id">
          <td>{{ emp.id }}</td>
          <td>{{ emp.name }}</td>
          <td>{{ emp.designation }}</td>
          <td>{{ emp.department }}</td>
          <td>{{ emp.salary }}</td>

          <td>
            <button @click="$emit('edit-employee', emp)" class="btn btn-warning btn-sm me-2">
              Edit
            </button>

            <button @click="remove(emp.id)" class="btn btn-danger btn-sm">
              Delete
            </button>
          </td>
        </tr>
      </tbody>
    </table>

    <p v-if="employees.length === 0" class="text-center">
      No employees found
    </p>
  </div>
</template>

<script>
import { deleteEmployee } from "../services/api";

export default {
  props: ["employees"],

  methods: {
    async remove(id) {
      if (confirm("Are you sure you want to delete?")) {
        await deleteEmployee(id);
        this.$emit("refresh-data");
      }
    }
  }
};
</script>