<template>
<b-form class="col-md-12" @submit="onFilter">
  <p class="notes">Note: filter the countries by the selected parametar here:</p>
    <div class="row">
      <b-form-group class="col-md-9">
          <select class="select form-control bg-dark text-light" v-model="filter">
                  <option value="Europe">Countries in Europe</option>
                  <option value="Asia">Countries in Asia </option>
                  <option value="Africa">Countries in Africa</option>
                  <option value="North America">Countries in North America</option>
                  <option value="South America">Countries in South America</option>
                  <option value="Safe">Safe countries</option>
                  <option value="Unsafe">Unsafe countries</option>
          </select>
    </b-form-group>
    <b-form-group class="col-md-3">
      <b-button type="submit" variant="dark" class="form-control">Filter</b-button>
    </b-form-group>
    </div>
    <table class="table table-striped table-dark table-sm">
      <thead class="thead-dark">
        <tr>
          <th>Country</th>
          <th>Capitol</th>
          <th>Population</th>
          <th>Continent</th>
          <th>Safety</th>
        </tr>
      </thead>
      <tbody  id="tbody_filter"></tbody>
    </table>
  </b-form>
</template>

<script>
import { bus } from '../components/event-bus';
  export default {
    data() {
      return {
        filter: 'Europe',
        filterArray: []
      }
      
    },
    created(){
      bus.$on('countriesArray', (countries) => {
      this.filterArray = countries
      })
    },
    methods: {
      safetyString(safeValue){
        if(safeValue === 1){
          return "Safe";
        }
        else if(safeValue === 2){
          return "Medium Safety";
        }
        else{
          return "Unsafe";
        }
      },
      buleanCheck(selection, continent, safety){
        if(selection === continent){
          return true
        }
        else if(selection === safety){
          return true
        }
        else {
          return false
        }
      },
      onFilter(event){
        event.preventDefault()
        let html = '';
         for(var i = 0; i < this.filterArray.length; i++){
           if(this.buleanCheck(this.filter, this.filterArray[i].continent, this.safetyString(this.filterArray[i].safety))){
             html += `<tr>
                        <td>${this.filterArray[i].country}</td>
                        <td>${this.filterArray[i].capitol}</td>
                        <td>${this.filterArray[i].population}</td>
                        <td>${this.filterArray[i].continent}</td>
                        <td>${this.safetyString(this.filterArray[i].safety)}</td>
                      </tr>`;
           }
         }
        document.getElementById('tbody_filter').innerHTML = html;
      },
    },
  }
</script>