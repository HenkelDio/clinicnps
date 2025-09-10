<template>
  <q-card class="nunito" flat bordered style="width: 600px; border-radius: 8px">
    <q-card-section class="row items-center justify-between">
      <div class="row q-gutter-x-sm items-center">
        <q-icon name="arrow_outward" color="grey-8" size="1rem" />
        <div class="text-subtitle1 text-weight-bold text-grey-8">Respostas por Mês</div>
      </div>
      <q-btn dense flat color="grey-9 nunito" no-caps>Ver mais ></q-btn>
    </q-card-section>

    <q-card-section class="row q-gutter-x-sm nunito">
      <div
        class="bg-green-2 row items-center justify-center"
        style="width: 20px; height: 20px; border-radius: 8px"
      >
        <q-icon name="arrow_outward" color="green-9" size="1rem" />
      </div>
      <div class="text-caption">10% mais respostas em relação ao mês passado</div>
    </q-card-section>

    <q-card-section class="flex flex-center">
      <div style="width: 500px; height: 300px">
        <BarChart :data="chartData" :options="chartOptions" />
      </div>
    </q-card-section>
  </q-card>
</template>

<script setup lang="ts">
import { computed } from 'vue';
import { Bar } from 'vue-chartjs'; // Importe o componente Bar
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  BarElement, // Adicione BarElement
  CategoryScale, // Adicione CategoryScale (eixo X)
  LinearScale, // Adicione LinearScale (eixo Y)
  type ChartData,
  type ChartOptions,
} from 'chart.js';

// Registre os novos elementos do gráfico de barras
ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale);

// Mude a interface e os dados para representar os meses
interface MonthlyData {
  label: string;
  value: number;
}

// Novos dados representando as respostas por mês
const monthlyData: MonthlyData[] = [
  { label: 'Jan', value: 80 },
  { label: 'Fev', value: 120 },
  { label: 'Mar', value: 95 },
  { label: 'Abr', value: 150 },
  { label: 'Mai', value: 110 },
  { label: 'Jun', value: 135 },
];

const chartData = computed<ChartData<'bar'>>(() => ({
  labels: monthlyData.map((item) => item.label),
  datasets: [
    {
      label: 'Total de Respostas',
      data: monthlyData.map((item) => item.value),
      backgroundColor: '#3057d7',
      borderRadius: 8,
    },
  ],
}));

// Opções para o gráfico de barras
const chartOptions = computed<ChartOptions<'bar'>>(() => ({
  responsive: true,
  maintainAspectRatio: false, // Para controlar o tamanho com o pai
  plugins: {
    legend: {
      display: false,
    },
    tooltip: {
      mode: 'index',
      intersect: false,
    },
  },
  scales: {
    x: {
      grid: {
        display: false,
      },
    },
    y: {
      beginAtZero: true,
      // Você pode ajustar as opções do eixo Y aqui
    },
  },
}));

// Renomeie a variável do componente
const BarChart = Bar;
</script>
