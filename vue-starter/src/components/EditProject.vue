<template>
  <div class="addproject">
    <bt/>
    <h1></h1>
    <h2></h2>
    <div class="col-lg-4"></div>
    <div class="col-lg-4">
      <form>
        
        <b-card-body class="pb-2">

      <b-form-group label="Tytuł">
        <b-input class="mb-1" v-model="project.title" />
      </b-form-group>

      <b-form-group label="Klient Sektor">
        <b-input class="mb-1" v-model="project.clientSector" />
      </b-form-group>

      <b-form-group label="Technologie">
        <b-select v-model="selectedtechnologies">
          <option v-for="techno in technologies">
            {{techno.technologyName}}
          </option>
        </b-select>
      </b-form-group>

      <b-form-group label="Data rozpoczęcia projektu">
        <b-input class="mb-1" />
      </b-form-group>

      <b-form-group label="Data zakończenia projektu">
        <b-input class="mb-1" />
      </b-form-group>

        <b-form-group label="Pracownik">
        <b-select v-model="selectedemployee">
          <option v-for="emp in employees">
            {{ emp.profile.name }} {{ emp.profile.lastName }}
          </option>
        </b-select>
      </b-form-group>

        


        <button type="submit" class="btn btn-primary btn-outline">Dodaj</button>
        <router-link to="/project">
          <button type="submit" class="btn btn-primary btn-outline">
            Wróć</button>
        </router-link>
        </b-card-body>
      </form>
    </div>
    <div class="col-lg-4"></div>
  </div>
  
</template>


<style src="vue-multiselect/dist/vue-multiselect.min.css"></style>
<style src="@/vendor/libs/vue-multiselect/vue-multiselect.scss" lang="scss"></style>

<!-- Page -->
<style src="@/vendor/styles/pages/users.scss" lang="scss"></style>

<script>
import axios from "axios";
import Vue from "vue";

import Multiselect from "vue-multiselect";

export default {
  // name: "Edit-Project",
  metaInfo: {
    title: "Edit Project"
  },
  components: {
    Multiselect
  },
  data: () => ({
    tableData: [],
    project: {
      title: "",
      clientSector: "",
      startDate: "",
      endDate: ""
    },
    employees: [],
    technologies: [],
    errors: [],
    selectedtechnologies: [],
    selectedemployee: [],
    errors: [],
    alert: "",
    file: null
  }),
  created() {
    var id = this.getUrlParameter("id");
    axios
      .get(`http://localhost:4444/api/projects/GetProject?id=` + id)
      .then(response => {
        this.project.title = response.data.title;
        this.project.clientSector = response.data.clientSector;
        this.project.startDate = response.data.startDate;
        this.project.endDate = response.data.endDate;
      })
      .catch(e => {
        this.errors.push(e);
      });
    axios
      .get("http://localhost:4444/api/technologies/GetTechnologies")
      .then(response => {
        this.technologies = response.data;
      })
      .catch(e => {
        this.errors.push(e);
      });
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
    getUrlParameter(name) {
      var results = new RegExp("[?&]" + name + "=([^&#]*)").exec(
        window.location.href
      );
      if (results == null) {
        return null;
      } else {
        return decodeURI(results[1]) || 0;
      }
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
</style>
