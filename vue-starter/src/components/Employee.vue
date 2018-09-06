<template>
   <div>
    <h4 class="font-weight-bold py-3 mb-4">
      <span class="text-muted font-weight-light">Pracownicy</span> / Developerzy
    </h4>

    <hr class="border-light container-m--x mt-0 mb-5">

    <v-client-table :data="employees" :columns='columns' :options="options">
      <template slot="edit" slot-scope="props">
        <div>
          <b-btn variant="outline-success borderless icon-btn" class="btn-xs" @click.prevent="cardEmployee(props.row.id)"><i class="ion ion-md-filing"></i></b-btn>
          <b-btn variant="outline-danger borderless icon-btn" class="btn-xs" @click.prevent="remove(props.row.id)"><i class="ion ion-md-close"></i></b-btn>
        </div>
      </template>
      <template slot="child_row" slot-scope="props">
        <div><b>First name:</b> {{props.row.name}}</div>
        <div><b>Last name:</b> {{props.row.lastName}}</div>
      </template>
    </v-client-table>
  </div>
</template>

<style src="@/vendor/libs/vue-data-tables/vue-data-tables.scss" lang="scss"></style>

<script>
import axios from "axios";
import Vue from "vue";
import router from "../router";

import { ClientTable } from "vue-tables-2";

Vue.use(ClientTable);

export default {
  name: "tables-vue-tables-2",
  metaInfo: {
    title: "Pracownicy"
  },
  data: () => ({
    tableData: [],
    employees: [],
    errors: [],
    alert: "",
    columns: ["name", "lastName", "edit"],
    options: {
      pagination: {
        chunk: 5
      },
      sortIcon: {
        is: "fa-sort",
        base: "fas",
        up: "fa-sort-up",
        down: "fa-sort-down"
      }
    }
  }),
  created() {
    axios
      .get("http://localhost:4444/api/employees/GetEmployees")
      .then(response => {
        this.employees = response.data;
      })
      .catch(e => {
        this.errors.push(e);
      });
  },
  methods: {
    edit(row) {
      alert(`Edit: ${row}`);
    },
    remove(row) {
      alert(`Remove: ${row}`);
    },
    cardEmployee(id) {
      router.push({
        path: `/card?id=` + id
      });
    }
  }
};
</script>
