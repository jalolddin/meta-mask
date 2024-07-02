<template>
  <div class="utilities">
    <h1>Блок-утилита</h1>
    <p v-if="encryptedResult">Encrypted/Decrypted Text: {{ encryptedResult }}</p>
    <textarea class="textarea" v-model="inputText" placeholder="Enter text"></textarea>
    <input
      class="input"
      v-model="encryptionKey"
      type="text"
      placeholder="Enter encryption key"
    />
    <button class="button" @click="encryptText">Encrypt Text</button>
    <button class="button" @click="decryptText">Decrypt Text</button>
  </div>
</template>

<script setup>
import CryptoJS from "crypto-js";
import { ref } from "vue";

const inputText = ref("");
const encryptionKey = ref("");
const encryptedResult = ref("");

const encryptText = () => {
  encryptedResult.value = CryptoJS.AES.encrypt(
    inputText.value,
    encryptionKey.value
  ).toString();
};

const decryptText = () => {
  const bytes = CryptoJS.AES.decrypt(encryptedResult.value, encryptionKey.value);
  inputText.value = bytes.toString(CryptoJS.enc.Utf8);
};
</script>

<style lang="scss">
.utilities {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  margin-top: 1rem;
  width: 30rem;
}
</style>
