<template>
  <q-page class="q-pa-lg">
    <div class="text-h5 nunito text-weight-bold">Usuários</div>

    <div class="row q-gutter-x-md q-mt-lg">
      <ModuleCard title="Usuários" icon="groups" actionText="Acessar" />
      <ModuleCard title="Departamentos" icon="corporate_fare" actionText="Acessar" />
    </div>
  </q-page>
</template>

<script setup lang="ts">
import ModuleCard from 'src/components/NPS/ModuleCard.vue';
</script>
