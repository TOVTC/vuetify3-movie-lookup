<script setup>
import router from '@/router';
import { ref } from 'vue';

const isFormValid = ref(false);
const searchTerm = ref('');
const validate = [
  () => {
      if (searchTerm.value.trim().length === 0) {
      return 'You must enter a valid search term';
    }
    return true;
  }
]

function submit() {
  if (!isFormValid.value) {
    return;
  }
  router.push({ name: 'Results', params: { term: searchTerm.value} });
}
</script>

<template>
  <v-container class="fill-height" fluid>
    <v-responsive class="align-center text-center fill-height">
      <v-row class="mt-5">
        <v-col cols="12" class="pa-5 text-center">
          <v-icon icon="mdi-movie-search" size="150" color="light-blue" class="ma-5" />
        </v-col>
      </v-row>
      <v-row>
        <v-spacer />
        <v-col cols="6" class="pa-5 text-center">
          <v-form v-model="isFormValid" @submit.prevent="submit">
            <v-text-field
              :rules="validate"
              v-model="searchTerm"
              label="Search for a movie"
              required
            />
            <v-btn type="submit" class="ma-3">Submit</v-btn>
          </v-form>
        </v-col>
        <v-spacer />
      </v-row>
    </v-responsive>
  </v-container>
</template>