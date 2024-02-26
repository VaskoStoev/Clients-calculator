<script setup>
import { computed, ref } from 'vue';
import '../assets/chartComponent.css';
const props = defineProps([
  'totalClients',
  'newClients',
  'newClientsPercent',
  'handleSubmit',
  'isSubmitDisabled',
]);

const series = computed(() => [props.newClientsPercent.toFixed(2)]);

const chartOptions = ref({
  chart: {
    height: 280,
    type: 'radialBar',
  },

  colors: ['#499fd7'],
  plotOptions: {
    radialBar: {
      hollow: {
        size: '70%',
      },
    },
  },

  labels: [''],
});
</script>

<template>
  <div class="chart-container">
    <div class="chart-body">
      <p>Percent Capacity: {{ props.newClientsPercent.toFixed(2) }}%</p>
      <Button
        :disabled="isSubmitDisabled"
        :class="{ disabled: isSubmitDisabled }"
        class="submit-button"
        @click="props.handleSubmit"
      >
        Submit
      </Button>
    </div>
    <apexchart width="500" type="radialBar" :options="chartOptions" :series="series"></apexchart>
  </div>
</template>
