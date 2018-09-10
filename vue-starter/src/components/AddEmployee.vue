<template>
  <div>
    <b-card-body class="pb-2">

      <b-form-group label="Imię">
        <b-input class="mb-1" />
      </b-form-group>

      <b-form-group label="Nazwisko">
        <b-input class="mb-1" />
      </b-form-group>

      <b-form-group label="Specjalizacja">
        <b-input class="mb-1" />
      </b-form-group>

      <b-form-group label="Ocena">
        <b-input class="mb-1" />
      </b-form-group>

      <b-form-group label="Kadencja">
        <b-input class="mb-1" />
      </b-form-group>

      <b-form-group label="Projekt">
        <b-select v-model="selectedproject" />
        <option v-for=" proj in projekts">
          {{proj.name}}
          </option>
      </b-form-group>

      <b-form-group label="Język">
        <b-select v-model="selectedlanguage" />
        <option v-for=" lang in languages">
          {{proj.languageName}}
        </option>
      </b-form-group>

      <b-form-group label="Stopień w mowie">
        <b-check-group v-model="multipleModel" :options="options" />
        <!-- <fieldset disabled>
            <b-radio-group v-model="singleModel" :options="options" />
          </fieldset> -->
      </b-form-group>

      <b-form-group label="Stopień w czytaniu">
        <b-check-group v-model="multipleModel" :options="options" />
      </b-form-group>

      <b-form-group label="Stopień w piśmie">
        <b-check-group v-model="multipleModel" :options="options" />
      </b-form-group>

      <b-form-group label="Umiejętności">
        <b-select v-model="selectedskill">
          <option v-for=" skil in skills">
            {{skil.skillName}}
          </option>
        </b-select>
      </b-form-group>

      <b-form-group label="Doświadczenie w latach">
        <b-input class="mb-1" />
      </b-form-group>

      <b-form-group label="Stopień">
        <b-check-group v-model="multipleModel" :options="options2" />
      </b-form-group>
    </b-card-body>
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
  name: "Add-EMployee",
  metaInfo: {
    title: "Add Employee"
  },
  components: {
    Multiselect
  },
  data: () => ({
    employees: [],
    languages: [],
    skills: [],
    projects: [],
    errors: [],
    selectedskill: [],
    selectedlanguage: [],
    selectedproject: [],
    errors: [],
    alert: "",
    options2: [
      {
        text: "1",
        value: "1"
      },
      {
        text: "2",
        value: "2"
      },
      {
        text: "3",
        value: "3"
      },
      {
        text: "4",
        value: "4"
      },
      {
        text: "5",
        value: "5"
      }
    ],
    options: [
      {
        text: "1",
        value: "1"
      },
      {
        text: "2",
        value: "2"
      },
      {
        text: "3",
        value: "3"
      }
    ],
    multipleModel: ["1"],
    file: null
  }),
  created() {
    axios
      .get("http://localhost:4444/api/languages/GetLanguages")
      .then(response => {
        this.languages = response.data;
      })
      .catch(e => {
        this.errors.push(e);
      });

    axios
      .get("http://localhost:4444/api/skills/GetSkills")
      .then(response => {
        this.skills = response.data;
      })
      .catch(e => {
        this.errors.push(e);
      });
    axios
      .get("http://localhost:4444/api/projects/GetProjects")
      .then(response => {
        this.projects = response.data;
      })
      .catch(e => {
        this.errors.push(e);
      });
  }
};
</script>
