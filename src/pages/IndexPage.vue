<template>
  <q-page class="column" style="padding: 30px">
    <div class="nunito row items-center q-gutter-x-md">
      <q-avatar color="primary" text-color="white">W</q-avatar>
      <div class="column">
        <div class="text-h6">Bem-vindo novamente, Willian</div>
        <div class="text-subtitle2 text-grey-8">Visualize as últimas respostas dos pacientes</div>
      </div>
    </div>

    <div>
      <!-- <q-card flat class="q-mb-lg" style="background-color: transparent; width: 400px">
        <q-card flat>
          <q-card-section class="row justify-between items-center">
            <div>
              <div class="text-subtitle1 text-grey-8">Pesquisas respondidas</div>
              <div class="text-h3 text-grey-9">{{ total }}</div>
            </div>
            <q-icon name="ballot" size="2rem" color="grey-9" />
          </q-card-section>
        </q-card>
      </q-card> -->

      <div class="q-my-lg row q-gutter-x-md">
        <DoughnutChartNPS />
        <BarChartNPS />
      </div>

      <q-card flat class="q-mb-lg" style="width: 1000px; background-color: transparent">
        <div class="row q-gutter-md">
          <q-card class="col-12 col-sm-3 bg-green-2" flat>
            <q-card-section class="row justify-between items-center">
              <div>
                <div class="text-subtitle2 text-green-9">Promotores</div>
                <div class="text-h4 text-grey-9">{{ promotores }}</div>
              </div>
              <q-icon name="mood" size="2rem" color="green-9" />
            </q-card-section>
          </q-card>
          <q-card class="col-12 col-sm-3 bg-yellow-2" flat>
            <q-card-section class="row justify-between items-center">
              <div>
                <div class="text-subtitle2 text-yellow-9">Neutros</div>
                <div class="text-h4 text-grey-9">{{ neutros }}</div>
              </div>
              <q-icon name="sentiment_neutral" size="2rem" color="yellow-9" />
            </q-card-section>
          </q-card>
          <q-card class="col-12 col-sm-3 bg-red-2" flat>
            <q-card-section class="row justify-between items-center">
              <div>
                <div class="text-subtitle2 text-red-9">Detratores</div>
                <div class="text-h4 text-grey-9">{{ detratores }}</div>
              </div>
              <q-icon name="sentiment_dissatisfied" size="2rem" color="red-9" />
            </q-card-section>
          </q-card>
        </div>
      </q-card>
    </div>
  </q-page>
</template>

<script setup lang="ts">
import { ref, computed, onMounted } from 'vue';
import type { ChartOptions } from 'chart.js';
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  LineElement,
  PointElement,
  CategoryScale,
  LinearScale,
} from 'chart.js';
import { Line } from 'vue-chartjs';
import DoughnutChartNPS from 'src/components/dashboard/DoughnutChartNPS.vue';
import BarChartNPS from 'src/components/dashboard/BarChartNPS.vue';

ChartJS.register(Title, Tooltip, Legend, LineElement, PointElement, CategoryScale, LinearScale);

const promotores = ref(120);
const neutros = ref(40);
const detratores = ref(20);
const total = ref(promotores.value + neutros.value + detratores.value);

const lineChartData = computed(() => ({
  labels: ['Janeiro', 'Fevereiro', 'Março', 'Abril', 'Maio', 'Junho'],
  datasets: [
    {
      label: 'NPS',
      data: [50, 60, 45, 70, 65, 80],
      fill: false,
      borderColor: '#1976D2',
      tension: 0.3,
    },
  ],
}));

const chartOptions: ChartOptions<'line'> = {
  responsive: true,
  plugins: {
    legend: {
      position: 'top',
    },
  },
};
</script>
