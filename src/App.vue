<template>
  <div class="container mt-4">
    <h1 class="text-center mb-4">Employee Management System</h1>

    <EmployeeForm
      :selectedEmployee="selectedEmployee"
      @add-employee="addEmp"
      @update-employee="updateEmp"
    />

    <EmployeeList
      :employees="employees"
      @edit-employee="editEmp"
      @refresh-data="fetchEmployees"
    />
  </div>
</template>

<script>
import EmployeeForm from "./components/EmployeeForm.vue";
import EmployeeList from "./components/EmployeeList.vue";
import {
  getEmployees,
  addEmployee,
  updateEmployee
} from "./services/api";

export default {
  components: {
    EmployeeForm,
    EmployeeList
  },

  data() {
    return {
      employees: [],
      selectedEmployee: null
    };
  },

  methods: {
    async fetchEmployees() {
      const res = await getEmployees();
      this.employees = res.data;
    },

    async addEmp(emp) {
      await addEmployee(emp);
      this.fetchEmployees();
    },

    async updateEmp(emp) {
      await updateEmployee(emp.id, emp);
      this.selectedEmployee = null;
      this.fetchEmployees();
    },

    editEmp(emp) {
      this.selectedEmployee = emp;
    }
  },

  mounted() {
    this.fetchEmployees();
  }
};
</script>