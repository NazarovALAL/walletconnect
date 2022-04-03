<template>
  <DefaultLayout>
    <WalletConnect></WalletConnect>
  </DefaultLayout>
</template>

<script lang="ts">
import Vue from 'vue';
import WalletConnect from './components/WalletConnect.vue';
import DefaultLayout from './layouts/DefaultLayout.vue';

export default Vue.extend({
  name: 'App',
  components: {
    WalletConnect,
    DefaultLayout
  }
});
</script>
