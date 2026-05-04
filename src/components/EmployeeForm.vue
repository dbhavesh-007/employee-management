<template>
  <div class="card p-3 mb-4">
    <h4>{{ isEdit ? "Update Employee" : "Add Employee" }}</h4>

    <input v-model="employee.name" placeholder="Name" class="form-control mb-2" />
    <input v-model="employee.designation" placeholder="Designation" class="form-control mb-2" />
    <input v-model="employee.department" placeholder="Department" class="form-control mb-2" />
    <input v-model="employee.salary" type="number" placeholder="Salary" class="form-control mb-2" />

    <button @click="submitData" class="btn btn-primary">
      {{ isEdit ? "Update" : "Add" }}
    </button>
  </div>
</template>

<script>
export default {
  props: ["selectedEmployee"],

  data() {
    return {
      employee: {
        name: "",
        designation: "",
        department: "",
        salary: ""
      },
      isEdit: false
    };
  },

  watch: {
    selectedEmployee(newVal) {
      if (newVal) {
        this.employee = { ...newVal };
        this.isEdit = true;
      }
    }
  },

  methods: {
    submitData() {
      if (this.isEdit) {
        this.$emit("update-employee", this.employee);
      } else {
        this.$emit("add-employee", this.employee);
      }

      this.employee = {
        name: "",
        designation: "",
        department: "",
        salary: ""
      };
      this.isEdit = false;
    }
  }
};
</script>