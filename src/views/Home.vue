<template>
  <div class="home-view-container">
    <h1> Adopt a new best friend. </h1>
    {{ getAllCats.length }}
    {{ animalsCount }}
    <b-row>
      <b-col lg="4" class="pb-2"><b-button @click="togglePetForm" pill variant="primary" size="lg">Add new Pet</b-button></b-col>
    </b-row>

    <b-card bg-variant="light" label-cols-lg="6">
      <b-form @submit.prevent="handleSubmit" v-if="showPetForm">
        <b-form-group
          label-cols-lg="3"
          label="Shipping Address"
          label-size="lg"
          label-class="font-weight-bold pt-0"
          class="mb-0"
        >
          <b-form-group label-cols-sm="3" label-align-sm="right" id="input-group-2" label="Pet's Name:" label-for="input-2">
            <b-form-input
              id="input-2"
              v-model="formData.name"
              required
              placeholder="Enter name"
            ></b-form-input>
          </b-form-group>
          <b-form-group label-cols-sm="3" label-align-sm="right" id="input-group-3" label="Species:" label-for="input-3">
            <b-form-select
              id="input-3" :options="['cats', 'dogs']" required v-model="formData.species" />
          </b-form-group>
          <b-form-group label-cols-sm="3" label-align-sm="right" id="input-group-2" label="Pet's Age:" label-for="input-2">
            <b-form-input
              type="number"
              id="input-2"
              v-model="formData.age"
              required
              placeholder="Enter age"
            ></b-form-input>
          </b-form-group>
        </b-form-group>
        <b-button type="submit" variant="primary">Submit</b-button>
        <b-button type="reset" variant="danger">Reset</b-button>
      </b-form>
    </b-card>
  </div>
</template>

<script>

import { mapActions, mapGetters } from 'vuex'

export default {

  name: 'home',
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
      'getAllCats'
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
      const { species, age, name } = this.formData
      const payload = {
        species,
        pet: {
          name,
          age
        }
      }
      this.addPet(payload)
      // reset form after submit
      this.formData = {
        name: '',
        age: 0,
        species: null
      }
    }
  }
}

</script>
