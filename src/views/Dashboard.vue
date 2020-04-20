<template>
  <div>
    <h1>Dashboard</h1>

    <EmployeesTable
      :employees="employees"
      @select-employee="setEmployee"
    ></EmployeesTable>

    <v-snackbar v-model="snackbar">
        You have selected {{ selectedEmployee.name }},
      {{ selectedEmployee.title }}
      <v-btn color="pink" text @click="snackbar = false">
        Close
      </v-btn>
    </v-snackbar>
  </div>
</template>

<script>
import EmployeesTable from "../components/EmployeesTable";
import employeesData from "../data/employees.json";

export default {
  name: "Dashboard",
  components: {
    EmployeesTable
  },
  data() {
    return {
      snackbar: false,
      currentItem: "",
      employees: employeesData,
      selectedEmployee: {
        name: "",
        title: ""
      }
    };
  },
  methods: {
    setEmployee(event) {
      this.snackbar = true;
      this.selectedEmployee.name = event.name;
      this.selectedEmployee.title = event.title;
    }
  }
};
</script>
<style>
</style>