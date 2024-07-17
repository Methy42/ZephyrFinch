<template>
  <div class="app-container">
    <ConnectPage v-if="currentPage == 'connect'" @connect-success="onConnectSuccess" />
    <CollectionPage v-if="currentPage == 'collection'" @collect-success="onCollectSuccess" />
    <EvaluationPage v-if="currentPage == 'evaluation'" @retry-evaluation="onRetryEvaluation" />
  </div>
</template>
<script setup lang="ts">
import { ref } from 'vue';

import ConnectPage from './pages/Connect.vue';
import CollectionPage from './pages/Collection.vue';
import EvaluationPage from './pages/Evaluation.vue';

const currentPage = ref<'connect' | 'collection' | 'evaluation'>('connect');

const onConnectSuccess = () => {
  currentPage.value = 'collection';
};

const onCollectSuccess = () => {
  currentPage.value = 'evaluation';
};

const onRetryEvaluation = () => {
  currentPage.value = 'collection';
};
</script>
<style scoped>
.app-container {
  width: 100vw;
  height: 100vh;

  background-color: #f7f7ff;
}
</style>
