<script setup>
import { computed, ref, watch } from 'vue';
import '../assets/inputComponent.css';
import ChartComponent from './ChartComponent.vue';

const totalClients = ref('');
const newClients = ref('');
const newClientsPercent = ref(0);
const error = ref(false);

watch([totalClients, newClients], ([newTotal, newNewClients]) => {
  if (newTotal && (isNaN(newTotal) || newTotal < 0)) {
    totalClients.value = '';
  }
  if (newNewClients && (isNaN(newNewClients) || newNewClients < 0)) {
    newClients.value = '';
  }
  if (newNewClients > newTotal) {
    newClients.value = newTotal;
    error.value = true;
    setTimeout(() => {
      error.value = false;
    }, 3000);
  }
  const total = Number(newTotal);
  const newCl = Number(newNewClients);
  if (total > 0) {
    newClientsPercent.value = (newCl / total) * 100;
  } else {
    newClientsPercent.value = 0;
  }
});
const isSubmitDisabled = computed(() => {
  return !(totalClients.value && newClients.value);
});
const handleSubmit = () => {
  if (!isSubmitDisabled.value) {
    alert(
      `Data submitted: Total Clients - ${totalClients.value}, New Clients - ${
        newClients.value
      }, Percent Capacity - ${newClientsPercent.value.toFixed(2)}%`
    );
    newClients.value = '';
    totalClients.value = '';
  }
};
</script>

<template>
  <div class="parent-container">
    <div class="input-container">
      <input type="number" placeholder="Total Clients" v-model.number="totalClients" />
      <input type="number" placeholder="New Clients" v-model.number="newClients" />
    </div>
  </div>
  <div v-if="error" style="margin-bottom: -40px">
    <p style="color: red; font-size: 13px">New clients cannot be more than the total number!</p>
  </div>
  <ChartComponent
    :totalClients="totalClients"
    :newClients="newClients"
    :newClientsPercent="newClientsPercent"
    :handleSubmit="handleSubmit"
    :isSubmitDisabled="isSubmitDisabled"
  />
</template>
