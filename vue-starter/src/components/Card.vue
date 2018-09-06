<template>
  <div>
    <div class="media align-items-center py-3 mb-3">
      <td>
        <img src="../assets/profile.jpg" alt="" class="d-block ui-w-150 rounded-circle">
      </td>
      <div class="media-body ml-4">
        <td style="padding-top: 100px">
          <h1 class="font-weight-bold mb-0">{{employee.profile.name}} {{employee.profile.lastName}} </h1>
        </td>
        <h2 class="font-weight-bold mb-0">{{employee.profile.specialization}}</h2>
        <table class="table-level">
          <table class="table table-hover" border="1">
            <td v-for="numb in 5" class="box-level " :key="numb">
              <div v-if="numb <= employee.profile.rating" class="box">
              </div>
            </td>
            <h5>
              <p style="color:gray">Rating:{{employee.profile.rating}} / 5</p>
            </h5>
          </table>
        </table>
        <tr>
          <td>
            <h5>
              <p style="color:gray">Overall Tenure:{{employee.profile.overallTenure}}year</p>
            </h5>
          </td>
        </tr>
        <b-btn variant="primary" size="sm">Edit</b-btn>&nbsp;
      </div>
    </div>
    <hr class="border-light container-m--x mt-0 mb-5">


    <h4 class="font-weight-bold py-3 mb-4">
      <span class="text-muted font-weight-light"></span>
    </h4>
    <v-client-table :data="empoyee" :columns='columns' :options="options">
      <template slot="edit" slot-scope="props">
        <div>
          <b-btn variant="outline-success borderless icon-btn" class="btn-xs" @click.prevent="cardEmployee(props.row.id)">
            <i class="ion ion-md-filing"></i>
          </b-btn>
          <b-btn variant="outline-danger borderless icon-btn" class="btn-xs" @click.prevent="remove(props.row.id)">
            <i class="ion ion-md-close"></i>
          </b-btn>
        </div>

      </template>
      <template slot="child_row" slot-scope="props">
        <div>
          <b>Umiejętności: </b> {{props.row.name}}</div>
        <div>
          <b>Doświadczenie: </b> {{props.row.experience}}</div>
        <div>
          <b>Stopień: </b> {{props.row.profficiency}}</div>
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
  name: "cartemployee",
  metaInfo: {
    title: "Karta Pracownika"
  },
  data: () => ({
    tableData: [],
    employee: {},
    errors: [],
    alert: "",
    columns: ["name", "experience", "profficiency", "edit"],
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
    var id = this.getUrlParameter("id");
    axios
      .get(`http://localhost:4444/api/employees/GetEmployee?id=` + id)
      .then(response => {
        this.employee = response.data;
      })
      .catch(e => {
        this.errors.push(e);
      });
  },
  methods: {
    getUrlParameter(name) {
      var results = new RegExp("[?&]" + name + "=([^&#]*)").exec(
        window.location.href
      );
      if (results == null) {
        return null;
      } else {
        return decodeURI(results[1]) || 0;
      }
    },
    edit(row) {
      alert(`Edit: ${row}`);
    },
    remove(row) {
      alert(`Remove: ${row}`);
    }
  }
};
</script>


<style scoped>
h1,
h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

.table-tittle {
  background: #f64a35;
}

.text-color {
  color: white;
}

.table-hover {
  border-color: lightgrey;
  border: lightgrey;
}

.level {
  color: gray;
  background: #f64a35;
  width: 100%;
  height: 100%;
}

.box-level {
  width: 20px;
  height: 20px;
}

.box {
  width: 100%;
  height: 100%;
  background: #f64a35;
}

.text-name {
  padding-top: 70px;
}
</style>
