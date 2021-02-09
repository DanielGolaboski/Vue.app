<template>
<b-form class="col-md-12" @submit="onSort">
  <p class="notes">Note: sort the countries by the selected parametar here:</p>
    <div class="row">
      <b-form-group class="col-md-9">
          <select class="select form-control bg-dark text-light" v-model="sort">
                  <option value="Most_populated">Sort by most populated</option>
                  <option value="Least_populated">Sort by least populated </option>
                  <option value="Safest">Safety(descending)</option>
                  <option value="Unsafest">Safety(ascending)</option>
          </select>
      </b-form-group>
      <b-form-group class="col-md-3">
        <b-button type="submit" variant="dark" class="form-control">Sort</b-button>
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
      <tbody id="tbody_sort"></tbody>
    </table>

  </b-form>
</template>

<script>
import { bus } from '../components/event-bus';
  export default {
    data() {
      return {
        sort: 'Most_populated',
        sortArray: []
      }
    },
    created(){
      bus.$on('countriesArray', (countries) => {
      this.sortArray = countries
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
      onSort(event){
        event.preventDefault()
        let array_sort = this.sortArray.map(item => item);

        if(this.sort === 'Most_populated'){
          array_sort.sort(function(a,b){ return b.population - a.population});
        }
        else if(this.sort === 'Least_populated'){
          array_sort.sort(function(a,b){ return a.population - b.population});
        }
        else if(this.sort === 'Safest'){
          array_sort.sort(function(a,b){ return a.safety - b.safety});
        }
        else{
          array_sort.sort(function(a,b){ return b.safety - a.safety });
        }
        let html = '';

        for(var i = 0; i < array_sort.length; i++){
          html += `<tr>
                      <td>${array_sort[i].country}</td>
                      <td>${array_sort[i].capitol}</td>
                      <td>${array_sort[i].population}</td>
                      <td>${array_sort[i].continent}</td>
                      <td>${this.safetyString(array_sort[i].safety)}</td>
                  </tr>`;
        }
        document.getElementById('tbody_sort').innerHTML = html;
        console.log(this.sortArray)
        console.log(array_sort)
      }
    }
  }
</script>