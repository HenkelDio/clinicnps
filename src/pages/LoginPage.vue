<template>
  <q-layout view="lHh Lpr lFf">
    <q-page-container>
      <q-page class="row justify-center" v-if="!showSplash">
        <q-card
          flat
          class="nunito flex flex-center q-pa-lg text-center login-card"
          style="width: 500px; max-width: 90vw"
        >
          <q-card-section style="width: 100%">
            <div class="text-h5 text-weight-medium q-mb-sm">Bem-vindo(a) ao</div>
            <q-img :src="logo_gray" width="130px" class="q-mb-md" />

            <div class="q-mt-md column q-gutter-y-md">
              <div>
                <div class="text-left">E-mail ou usuário</div>
                <q-input v-model="user" outlined dense placeholder="E-mail ou usuário" />
              </div>

              <div>
                <div class="text-left">Senha</div>
                <q-input
                  v-model="password"
                  outlined
                  dense
                  placeholder="Mín. 8 caracteres"
                  type="password"
                />
              </div>

              <div class="row justify-between">
                <q-checkbox v-model="rememberMe" label="Lembre de mim" />
                <q-btn flat label="Esqueceu sua senha?" dense no-caps color="primary" />
              </div>

              <q-btn
                label="Login"
                no-caps
                color="primary"
                unelevated
                class="q-mt-xl"
                @click="showSplashScreen"
              />
            </div>
          </q-card-section>
        </q-card>

        <div class="bg-primary col lt-lg-hide flex text-white q-pa-xl text-container">
          <div>
            <div><q-img :src="logo_icon" width="100px" class="q-mb-md" /></div>
            <div class="text-h3 text-weight-bold nunito">Conecte. Entenda. Fidelize</div>
            <div class="text-subtitle1 q-mt-md">
              Transforme feedback em cuidado de excelência para hospitais e clínicas.
            </div>
          </div>
        </div>
      </q-page>

      <q-page
        v-else
        style="width: 100%; height: 100%"
        class="row justify-center items-center bg-primary column"
      >
        <div><q-img :src="logo_icon" width="100px" class="q-mb-md" /></div>
        <div><q-img :src="logo_white" width="130px" class="q-mb-md" /></div>
        <div class="q-mt-md">
          <q-circular-progress indeterminate rounded size="50px" color="white" class="q-ma-md" />
        </div>
      </q-page>
    </q-page-container>
  </q-layout>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import logo_gray from '../assets/logo/logo_gray.svg';
import logo_white from '../assets/logo/logo_white.svg';
import logo_icon from '../assets/icons/icon.png';
import { useRouter } from 'vue-router';

const user = ref('');
const password = ref('');
const rememberMe = ref(false);
const showSplash = ref(false);

const router = useRouter();

const showSplashScreen = () => {
  showSplash.value = true;
  setTimeout(() => {
    showSplash.value = false;
    router.push({ path: '/dashboard' }).catch((err) => {
      console.error('Erro ao navegar:', err);
    });
  }, 1000);
};
</script>

<style scoped>
@media (max-width: 600px) {
  .text-container {
    display: none !important;
  }

  .login-card {
    padding: 0px !important;
  }
}

.page-limit {
  max-width: 1680px;
  max-height: 600px;
  margin: auto;
  width: 100%;
  height: 100%;
}

.text-container {
  line-height: 1.4;
}
</style>
