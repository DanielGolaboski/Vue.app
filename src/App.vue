<template>
  <div id="app">

    <b-container class="bv-example-row">
      <h5 class="description">You can submit a few countries in the form on the left and display your resoults in the tables on the right</h5>
      <b-row>
        <b-col md="3">
          <AddCountry  />
        </b-col>
        <b-col md="9">
          <b-row>
            <b-col md="12">
              <SortCountries  />
            </b-col>
          </b-row>
          <b-row>
            <b-col md="12">
              <FilterCountries  />
            </b-col>
          </b-row>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import AddCountry from './components/AddCountry.vue'
import SortCountries from './components/SortCountries.vue'
import FilterCountries from './components/FilterCountries.vue'

export default {
  name: 'App',
  components: {
    AddCountry,
    SortCountries,
    FilterCountries
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding-top: 20px;
  background-color: #ada5a5;
  height: 100vh;
}
.description {
  padding-bottom: 20px;
  margin-bottom: 30px;;
  border-bottom: 1px solid rgb(48, 43, 43);
}
.notes{
  text-align: left;
}
</style>
