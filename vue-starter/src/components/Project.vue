<template>
  <div>
    <h4 class="font-weight-bold py-3 mb-4">
      <span class="text-muted font-weight-light"></span>Projekty
    </h4>

    <hr class="border-light container-m--x mt-0 mb-5">

    <v-client-table :data="projects" :columns='columns' :options="options">
      <template slot="edit" slot-scope="props">
        <div>
          <b-btn variant="outline-success borderless icon-btn" class="btn-xs" @click.prevent="edit(props.row.id)">
            <i class="ion ion-md-create"></i>
          </b-btn>
          <b-btn variant="outline-danger borderless icon-btn" class="btn-xs" @click.prevent="remove(props.row.id)">
            <i class="ion ion-md-close"></i>
          </b-btn>
        </div>
      </template>
      <template slot="child_row" slot-scope="props">
        <div>
          <b>Nazwa:</b> {{props.row.name}}</div>
        <div>
          <b>Tytuł:</b> {{props.row.title}}</div>
        <div>
          <b>Klient Sektor:</b> {{props.row.clientSector}}</div>
        <div>
          <b>Technologie:</b> {{props.row.technology}}</div>
        <div>
          <b>Start:</b> {{props.row.startDate}}</div>
        <div>
          <b>Koniec:</b> {{props.row.endDate}}</div>
      </template>
    </v-client-table>
  </div>
</template>

<style src="@/vendor/libs/vue-data-tables/vue-data-tables.scss" lang="scss"></style>

<script>
import axios from "axios";
import Vue from "vue";
import { ClientTable } from "vue-tables-2";

Vue.use(ClientTable);

export default {
  name: "tables-vue-tables-2",
  metaInfo: {
    title: "Projekty"
  },
  data: () => ({
    tableData: [],
    projects: [],
    errors: [],
    alert: "",
    columns: ["name", "title", "edit"],
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
      .get(`http://localhost:4444/api/projects/GetProjects`)
      .then(response => {
        this.projects = response.data;
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
    }
  }
};
</script>
