<template>
  <div>
    <h1>Lista pacjentów</h1>
    <div v-for="patient in patients" v-bind:key="patient.id">
      <p class="patient">{{ patient.name }} {{ patient.lastName }}</p>
      <div
        class="medicine"
        v-for="medicine in medicines"
        v-bind:key="medicine.id"
      >
        {{
          medicine.patientIds[0] === patient.id ? medicine.medicationName : null
        }}
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
          console.log(this.patients);
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
          console.log(this.medicines);
        })
        .catch((error) => {
          console.log(error);
        });
    },

    filterPatients30() {},
    filterPatients83() {},
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
</style>
