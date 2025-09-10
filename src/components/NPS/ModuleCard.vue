<template>
  <q-card flat bordered style="width: 300px">
    <q-card-section class="nunito row q-gutter-x-sm items-center">
      <div class="bg-grey-2 row justify-center items-center" style="width: 20px; height: 20px">
        <q-icon :name="props.icon" class="text-grey-7"></q-icon>
      </div>
      <div class="text-subtitle1 text-grey-9">{{ props.title }}</div>
    </q-card-section>
    <q-card-actions>
      <q-btn no-caps unelevated class="bg-primary" color="text-white">{{ props.actionText }}</q-btn>
    </q-card-actions>
  </q-card>
</template>
<script setup lang="ts">
interface IProps {
  title: string;
  icon: string;
  actionText: string;
}

const props = defineProps<IProps>();
</script>
