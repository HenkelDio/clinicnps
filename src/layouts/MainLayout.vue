<template>
  <q-layout view="lHh Lpr lFf">
    <!-- <q-header class="q-ml-md text-black sansation q-pa-sm" style="background-color: #fafafa">
      <q-toolbar>
        <q-toolbar-title class="column">
          <div class="row items-center q-gutter-x-sm text-grey-9">
            <q-icon :name="header?.icon" size="1.6rem" />
            <div style="font-weight: bold">{{ header?.title }}</div>
          </div>
          <div class="text-body2 text-grey-8">{{ header?.subtitle }}</div>
        </q-toolbar-title>
      </q-toolbar>
    </q-header> -->

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      :mini="false"
      class="custom-drawer"
      :width="260"
    >
      <div class="row items-center justify-center q-pa-md q-mt-md">
        <q-img :src="logo" width="150px"></q-img>
      </div>

      <div
        class="row justify-between items-center q-pa-sm q-ma-md nunito"
        style="border: 1px solid #f0f0f0; border-radius: 8px"
      >
        <div class="row q-gutter-x-sm items-center">
          <div
            class="bg-grey-9 row items-center justify-center"
            style="border-radius: 50px; width: 30px; height: 30px"
          >
            <q-icon name="apartment" color="grey-1" size="1rem" />
          </div>
          <div>
            <div class="text-subtitle2 text-grey-9">Hospital do Willian</div>
            <div class="text-caption">Estabelecimento</div>
          </div>
        </div>
        <div>
          <q-btn icon="swap_vert" flat class="bg-grey-3 text-grey-8" dense>
            <q-tooltip>Mudar de estabelecimento</q-tooltip>

            <q-menu anchor="bottom start">
              <q-list style="min-width: 100px">
                <q-item clickable v-close-popup>
                  <q-item-section>
                    <q-item-label>Hospital do Willian</q-item-label>
                    <q-item-label caption>Atual</q-item-label>
                  </q-item-section>
                </q-item>
              </q-list>
            </q-menu>
          </q-btn>
        </div>
      </div>

      <q-list class="column justify-between q-pa-md">
        <div>
          <EssentialLink
            v-for="link in linksList"
            :key="link.title"
            v-bind="link"
            class="q-mb-sm"
          />
        </div>

        <div class="q-mt-lg">
          <div class="text-caption text-grey-9 q-mb-sm">Configurações</div>
          <EssentialLink
            v-for="link in linksBottomList"
            :key="link.title"
            v-bind="link"
            class="q-mb-sm"
          />
        </div>
      </q-list>
    </q-drawer>

    <q-page-container style="background-color: #fafafa">
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup lang="ts">
import { computed, ref } from 'vue';
import EssentialLink, { type EssentialLinkProps } from 'components/EssentialLink.vue';
import { useRoute } from 'vue-router';
import logo from '../assets/logo/logo_gray.svg';

const route = useRoute();

const linksList: EssentialLinkProps[] = [
  {
    title: 'Dashboard',
    icon: 'analytics',
    link: '/dashboard',
    subtitle: 'Acompanhe  as últimas respostas dos seus pacientes',
  },
  {
    title: 'NPS',
    icon: 'ballot',
    caption: 'Gerencie e envie pesquisas',
    link: '/nps',
  },
  {
    title: 'Usuários',
    icon: 'groups',
    caption: 'Crie e edite usuários',
    link: '/users',
  },
];

const linksBottomList: EssentialLinkProps[] = [
  {
    title: 'Meu perfil',
    icon: 'account_circle',
    link: '/profile',
  },
  {
    title: 'Configurações',
    icon: 'settings_applications',
    link: '/profile',
  },
  {
    title: 'Sair',
    icon: 'power_settings_new',
    link: '/',
  },
];

const leftDrawerOpen = ref(false);

const header = computed(() => {
  return linksList.filter((link) => link.link === route.path)[0];
});
</script>

<style lang="scss">
.custom-drawer {
  border-right: 1px solid #f0f0f0;
}
</style>
