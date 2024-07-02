<template>
  <div class="get-result">
    <textarea class="textarea" v-model="inputText" placeholder="Enter text"></textarea>
    <button class="button" @click="calculateSHA256">Get SHA256</button>
    <p v-if="hashResult">SHA256: {{ hashResult }}</p>
  </div>
</template>

<script setup>
import CryptoJS from "crypto-js";
import { ref } from "vue";

const hashResult = ref("");
const inputText = ref("");
const calculateSHA256 = () => {
  hashResult.value = CryptoJS.SHA256(inputText.value).toString(CryptoJS.enc.Hex);
};
</script>

<style lang="scss">
.get-result {
  display: flex;
  flex-direction: column;
  width: 30rem;
  margin-top: 1.5rem;
  gap: 1.5rem;
}
</style>
