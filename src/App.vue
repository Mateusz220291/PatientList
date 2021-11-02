<template>
  <div>
    <h1>Lista pacjentów</h1>

    <div class="container" v-for="patient in patients" v-bind:key="patient.id">
      <div class="patient">
        Imię i nazwisko:{{ patient.name }} {{ patient.lastName }}
      </div>
      <h1>LEKI:</h1>
      <div v-for="medicine in medicines" v-bind:key="medicine.id">
        <h1 v-if="medicine.patientIds.includes(patient.id)">
          {{ medicine.medicationName }}
        </h1>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      patients: [],
      medicines: [],
    };
  },

  methods: {
    getPatients() {
      axios
        .get("https://cerber.pixel.com.pl/api/patients")
        .then((response) => {
          this.patients = response.data;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    getMedicines() {
      axios
        .get("https://cerber.pixel.com.pl/api/medicine")
        .then((response) => {
          this.medicines = response.data;
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
  beforeMount() {
    this.getPatients();
    this.getMedicines();
  },
};
</script>

<style scoped>
.patient {
  color: red;
}
.container {
}
</style>
