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
        <b-input class="mb-1" />
      </b-form-group>

      <b-form-group label="Klient Sektor">
        <b-input class="mb-1" />
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
