<template>
  <v-app>
    <AppHeader/>
    <v-main>
      <slot></slot>
    </v-main>
  </v-app>
</template>

<script lang="ts">
import Vue from 'vue';
import AppHeader from '@/components/AppHeader.vue';

export default Vue.extend({
  name: 'DefaultLayout',
  components: {
    AppHeader
  }
});
</script>