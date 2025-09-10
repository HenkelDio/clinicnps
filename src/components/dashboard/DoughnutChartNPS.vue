<template>
  <q-card class="nunito" flat bordered style="width: 400px; border-radius: 8px">
    <q-card-section class="row items-center justify-between">
      <div class="row q-gutter-x-sm items-center">
        <q-icon name="article" color="grey-8" size="1rem" />
        <div class="text-subtitle1 text-weight-bold text-grey-8">Pesquisas NPS</div>
      </div>
      <q-btn dense flat color="grey-9 nunito" no-caps>Ver mais ></q-btn>
    </q-card-section>

    <!-- Gráfico -->
    <q-card-section class="flex flex-center">
      <div style="width: 200px; height: 200px; position: relative">
        <DoughnutChart :data="chartData" :options="chartOptions" />
        <!-- Valor no centro -->
        <div class="absolute-full flex flex-center column text-center" style="pointer-events: none">
          <div class="text-h6 text-grey-8">Score</div>
          <div class="text-h5 text-weight-bold">
            {{ npsScore }}
          </div>
        </div>
      </div>
    </q-card-section>

    <q-separator />

    <!-- Lista de detalhes -->
    <q-list bordered separator>
      <q-item v-for="(item, index) in npsCategories" :key="index">
        <q-item-section avatar>
          <q-icon name="circle" :style="{ color: item.color }" />
        </q-item-section>
        <q-item-section>{{ item.label }}</q-item-section>
        <q-item-section side class="text-weight-bold">
          {{ item.value }}
        </q-item-section>
      </q-item>
    </q-list>
  </q-card>
</template>

<script setup lang="ts">
import { computed } from 'vue';
import { Doughnut } from 'vue-chartjs';
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  ArcElement,
  type ChartData,
  type ChartOptions,
} from 'chart.js';

ChartJS.register(Title, Tooltip, Legend, ArcElement);

interface NpsCategory {
  label: string;
  value: number;
  color: string;
}

const npsCategories: NpsCategory[] = [
  { label: 'Promotores', value: 120, color: '#8AC926' },
  { label: 'Neutros', value: 60, color: '#FFCA3A' },
  { label: 'Detratores', value: 20, color: '#FF595E' },
];

const chartData = computed<ChartData<'doughnut'>>(() => ({
  labels: npsCategories.map((item) => item.label),
  datasets: [
    {
      data: npsCategories.map((item) => item.value),
      backgroundColor: npsCategories.map((item) => item.color),
      borderWidth: 2,
    },
  ],
}));

const chartOptions = computed<ChartOptions<'doughnut'>>(() => ({
  responsive: true,
  cutout: '60%',
  plugins: {
    legend: {
      display: false,
    },
  },
}));

const npsScore = computed(() => {
  const promotores = npsCategories[0]?.value ?? 0;
  const detratores = npsCategories[2]?.value ?? 0;
  const total = npsCategories.reduce((sum, i) => sum + i.value, 0);
  return total > 0 ? Math.round(((promotores - detratores) / total) * 100) : 0;
});

const DoughnutChart = Doughnut;
</script>
