<template>
  <div class="panel">
    <h1>Док панель</h1>
    <div>
      <button
        class="button"
        v-for="app in apps"
        :key="app.name"
        @click="openApp(app.url)"
      >
        {{ app.name }}
      </button>
    </div>
  </div>
  <iframe
    v-if="selectedApp"
    :src="selectedApp"
    style="width: 100%; height: 600px"
  ></iframe>
</template>

<script setup>
import { ref } from "vue";

const apps = ref([
  { name: "Uniswap", url: "https://app.uniswap.org/" },
  { name: "1inch", url: "https://app.1inch.io/" },
  { name: "Bugs Denet", url: "https://bugs.denet.pro/" },
  { name: "Revert Finance", url: "https://revert.finance/" },
]);

const selectedApp = ref(null);

const openApp = (url) => {
  selectedApp.value = url;
};
</script>

<style lang="scss">
.panel {
  width: 30rem;
  display: flex;
  flex-direction: column;
  gap: 1rem;
  div {
    display: flex;
    justify-content: space-between;
  }
}
</style>
