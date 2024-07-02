<template>
  <div class="connect-wallet">
    <h1>Подключение кошелька Metamask</h1>
    <button class="button" @click="connectMetamask">Connect Metamask</button>
    <p v-if="account">Connected Account: {{ account }}</p>
    <p v-if="account && !extensionOpened">
      MetaMask connected! Click below to open the extension and manage your transactions.
      <button class="button" @click="openMetaMaskExtension">
        Open MetaMask Extension
      </button>
    </p>
    <p v-if="!account && metamaskDetected">
      Please connect MetaMask to manage your transactions.
    </p>
    <p v-if="!metamaskDetected">
      MetaMask not detected. Please install MetaMask extension.
    </p>
  </div>
</template>

<script setup>
import { ref } from "vue";

const account = ref(null);
const metamaskDetected = ref(false);
const extensionOpened = ref(false);
const openMetaMaskExtension = () => {
  window.open("chrome-extension://nkbihfbeogaeaoehlefnkodbefgpgknn/home.html");
  extensionOpened.value = true;
};
const connectMetamask = async () => {
  if (window.ethereum) {
    try {
      await window.ethereum.request({ method: "eth_requestAccounts" });
      const accounts = await ethereum.request({ method: "eth_accounts" });
      account.value = accounts[0];
    } catch (error) {
      console.error(error);
    }
  } else {
    metamaskDetected.value = false;
    alert("Metamask not detected. Please install Metamask extension.");
  }
};
</script>

<style lang="scss">
.connect-wallet {
  display: flex;
  width: 30rem;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>
