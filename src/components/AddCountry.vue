<template>
  <b-form class="col-md-12" @submit="onSubmit">
    <b-form-group>
      <label>Country</label>
      <input class="inputs bg-dark text-light" type="text" pattern="[A-Za-z\s]{3,}" title="Please enter 3 or more characters, alphabet letters only" required v-model="country">
    </b-form-group>
    <b-form-group>
      <label>Capitol</label>
      <input class="inputs bg-dark text-light" type="text" pattern="[A-Za-z\s]{3,}" title="Please enter 3 or more characters, alphabet letters only" required v-model="capitol">
    </b-form-group>
    <b-form-group>
      <label>Population</label>
      <input class="inputs bg-dark text-light" type="number" required v-model="population">
    </b-form-group>
    <b-form-group>
      <label>Continent</label>
        <select class="select bg-dark text-light" v-model="continent">
          <option value="Europe">Europe</option>
          <option value="Asia">Asia</option>
          <option value="Africa">Africa</option>
          <option value="South America">South America</option>
          <option value="North America">Norht America</option>
        </select>
    </b-form-group>
    <b-form-group>
      <label>Safety</label>
        <select class="select bg-dark text-light" v-model="safety">
          <option value="Safe">Safe</option>
          <option value="Medium Safety">Medium Safety</option>
          <option value="Unsafe">Unsafe</option>
        </select>
    </b-form-group>

    <b-button type="submit" variant="dark">Submit</b-button>
  </b-form>

  
</template>

<script>
import { bus } from '../components/event-bus';
export default {

  data(){
    return{
      country: '',
      capitol: '',
      population: '',
      continent: 'Europe',
      safety: 'Safe',
      sort: '',
      countries:[]
    }
  },
  methods: {
    safetySort(){
        if(this.safety === 'Safe'){
          return 1;
        }
        else if (this.safety === 'Medium Safety'){
          return 2;
        }
        else {
          return 3;
        }
    },
    
    onSubmit(event) {
        event.preventDefault()
        var newCountry = {
          country:this.country,
          capitol:this.capitol,
          population:this.population,
          continent:this.continent,
          safety:this.safetySort(),
          
          sort:this.sort
        };
        this.country = '',
        this.capitol = '',
        this.population = '',
        this.continent = 'Europe',
        this.safety = 'Safe',
        this.countries.push(newCountry),
        bus.$emit('countriesArray', this.countries)
      },
  }
}
</script>

<style scoped>
   .select, .inputs{
     width: 100%;
     border-radius: 2px;
     padding: 10px 5px;
     border: 1px solid rgb(109, 107, 107);
     outline: none;
   }

</style>