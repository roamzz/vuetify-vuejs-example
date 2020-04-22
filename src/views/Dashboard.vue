<template>
  <v-container>
    <h1>Dashboard</h1>

    <v-row>
      <v-col v-for="(sale, index) in sales" :key="index" cols="12" md="4">
        <SalesGraph :sale="sale"></SalesGraph>
      </v-col>
    </v-row>

    <v-row>
      <v-col
        v-for="(statistic, index) in statistics"
        :key="index"
        cols="12"
        md="6"
        lg="3"
      >
        <StatisticCard :statistic="statistic"></StatisticCard>
      </v-col>
    </v-row>

    <v-row>
      <v-col cols="12" md="8">
        <EmployeesTable
          :employees="employees"
          @select-employee="setEmployee"
        ></EmployeesTable>
      </v-col>

      <v-col cols="12" md="4">
        <EventTimeline :timeline="timeline"></EventTimeline>
      </v-col>
    </v-row>

    <v-row id="below-the-fold" v-intersect="showMoreContent">
      <v-col cols="12" md="8">
        <EmployeesTable :employees="employees" @select-employee="setEmployee" />
      </v-col>
      <v-col cols="12" md="4">
        <EventTimeline :timeline="timeline" />
      </v-col>
    </v-row>

    <v-row v-if="loadNewContent" id="more-content">
      <v-col>
        <v-skeleton-loader
          ref="skeleton"
          type="table"
          class="mx-auto"
        ></v-skeleton-loader>
      </v-col>
    </v-row>

    <v-snackbar v-model="snackbar" :left="$vuetify.breakpoint.mdAndUp">
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
import StatisticCard from "../components/StatisticCard";
import statisticsData from "../data/statistics.json";
import SalesGraph from "../components/SalesGraph";
import salesData from "../data/sales.json";




export default {
  name: "Dashboard",
  components: {
    EmployeesTable,
    EventTimeline,
    StatisticCard,
    SalesGraph,

  },
  data() {
    return {
      loadNewContent: false,
      snackbar: false,
      currentItem: "",
      employees: employeesData,
      timeline: timelineData,
      statistics: statisticsData,
      sales: salesData,
      selectedEmployee: {
        name: "",
        title: ""
      }
    };
  },
  methods: {
    showMoreContent(entries) {
      this.loadNewContent = entries[0].isIntersecting;
    },

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