<template>
  <q-item
    clickable
    @click="$router.push({ path: link })"
    :class="`nunito bg-${isActive ? 'grey-2' : 'white'} rounded-borders`"
    style="font-weight: bold"
  >
    <q-item-section v-if="icon" avatar>
      <q-icon :name="icon" :color="isActive ? 'primary' : 'grey-8'" />
    </q-item-section>

    <q-item-section>
      <q-item-label :class="`text-${isActive ? 'primary' : 'black-8'}`">{{ title }}</q-item-label>
    </q-item-section>

    <q-tooltip anchor="top right" class="bg-grey-9" v-if="caption"> {{ caption }} </q-tooltip>
  </q-item>
</template>

<script setup lang="ts">
import { computed } from 'vue';
import { useRoute } from 'vue-router';

const route = useRoute();

export interface EssentialLinkProps {
  title: string;
  caption?: string;
  link?: string;
  icon?: string;
  subtitle?: string;
}

const props = withDefaults(defineProps<EssentialLinkProps>(), {
  caption: '',
  link: '#',
  icon: '',
});

const isActive = computed(() => route.path === props.link);
</script>
