<template>
  <div class="home-view-container">
    <h1>Adopt a New Best Friend</h1>
    Number of Cats: {{ getAllCats.length }} <br>
    Number of Dogs: {{ getAllDogs.length }} <br>
    Total Number of Pets: {{ animalsCount }} <br><br>

    <button @click="togglePetForm" class="btn btn-primary">Add New Pet</button> <br><br>

    <b-form @submit.prevent="handleSubmit" v-if="showPetForm">
      <b-form-group id="input-group-1" label="Pet's Name:" label-for="input-1">
        <b-form-input
          id="input-1"
          v-model="formData.name"
          required
          placeholder="Enter name"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-2" label="Breed:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="formData.breed"
          required
          placeholder="Enter breed"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-3" label="Species:" label-for="input-3">
        <b-form-select
          id="input-3"
          v-model="formData.species"
          :options="['cats','dogs']"
          required
        ></b-form-select>
      </b-form-group>

      <b-form-group id="input-group-4" label="Gender:" label-for="input-4">
        <b-form-select
          id="input-4"
          v-model="formData.gender"
          :options="['male','female']"
          required
        ></b-form-select>
      </b-form-group>

      <b-form-group id="input-group-5" label="Age:" label-for="input-5">
        <b-form-input
          id="input-5"
          type="number"
          v-model="formData.age"
          required
          placeholder="Enter Age"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-6" label="Color:" label-for="input-6">
        <b-form-input
          id="input-6"
          v-model="formData.color"
          required
          placeholder="Enter color"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-7" label="Weight:" label-for="input-7">
        <b-form-input
          id="input-7"
          type="number"
          v-model="formData.weight"
          required
          placeholder="Enter weight"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-8" label="Location:" label-for="input-8">
        <b-form-input
          id="input-8"
          v-model="formData.location"
          required
          placeholder="Enter location"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-9" label="Notes:" label-for="input-9">
        <b-form-input
          id="input-9"
          v-model="formData.notes"
          required
          placeholder="Enter notes"
        ></b-form-input>
      </b-form-group>

    <b-button type="submit" variant="primary" style="margin: 0 1%">Submit</b-button>
    <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
  </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'

export default {
  name: 'Home',
  data () {
    return {
      showPetForm: false,
      formData: {
        name: '',
        age: 0,
        species: null
      }
    }
  },
  computed: {
    ...mapGetters([
      'animalsCount',
      'getAllCats',
      'getAllDogs'
    ])
  },
  methods: {
    ...mapActions([
      'addPet'
    ]),
    togglePetForm () {
      this.showPetForm = !this.showPetForm
    },
    handleSubmit () {
      const { species, age, name, breed, color, weight, location, notes, gender } = this.formData
      const payload = {
        species,
        pet: {
          name,
          age,
          species,
          breed,
          color,
          weight,
          location,
          notes,
          gender
        }
      }
      this.addPet(payload)

      // resets the add pet form
      this.formData = {
        name: '',
        age: 0,
        species: null,
        breed: '',
        color: '',
        weight: 0,
        location: '',
        notes: '',
        gender: ''
      }
    }
  }
}
</script>
