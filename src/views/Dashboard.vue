<template>
  <v-container>
    <h1>Dashboard</h1>

    <v-row>
      <v-col cols="8">
        <EmployeesTable
          :employees="employees"
          @select-employee="setEmployee"
        ></EmployeesTable>
      </v-col>

      <v-col cols="4">
        <EventTimeline :timeline="timeline"></EventTimeline>
      </v-col>
    </v-row>

    <v-snackbar v-model="snackbar">
      You have selected {{ selectedEmployee.name }},
      {{ selectedEmployee.title }}
      <v-btn color="pink" text @click="snackbar = false">
        Close
      </v-btn>
    </v-snackbar>
  </v-container>
</template>

<script>
import EmployeesTable from "../components/EmployeesTable";
import employeesData from "../data/employees.json";

import EventTimeline from "../components/EventTimeline";
import timelineData from "../data/timeline.json";

export default {
  name: "Dashboard",
  components: {
    EmployeesTable,
    EventTimeline
  },
  data() {
    return {
      snackbar: false,
      currentItem: "",
      employees: employeesData,
      timeline: timelineData,
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