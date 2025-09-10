<template>
  <q-page class="q-pa-lg">
    <div class="text-h5 nunito text-weight-bold">Net Promoter Score</div>

    <div class="row q-gutter-x-md q-mt-lg">
      <ModuleCard
        title="Novo envio de pesquisa NPS"
        icon="arrow_upload_ready"
        actionText="Enviar"
      />
      <ModuleCard title="Respostas dos pacientes" icon="article" actionText="Acessar" />
      <ModuleCard title="Histórico de envios" icon="history" actionText="Acessar" />
    </div>

    <q-separator class="q-my-xl" />

    <div class="text-h5 nunito text-weight-bold">Formulários</div>

    <div class="row q-gutter-x-md q-mt-lg">
      <ModuleCard title="Formulários" icon="arrow_upload_ready" actionText="Acessar" />
    </div>
  </q-page>
</template>

<script setup lang="ts">
import ModuleCard from 'src/components/NPS/ModuleCard.vue';
</script>
