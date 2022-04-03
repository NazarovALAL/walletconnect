<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12" class="mt-10">
        <h1 v-if="isConnected" class="display-2 font-weight-bold mb-3">
          You connected to trust wallet
        </h1>
        <h1 v-else class="display-2 font-weight-bold mb-3">
          Connect to your wallet
        </h1>
      </v-col>
      <v-col cols="12">
        <div v-if="isConnected">
          <div class="mb-5">Your Address: {{ address }}</div>
          <v-btn @click="disconnect" color="black" class="white--text" large>
            Disconnect
          </v-btn>
        </div>
        <div v-else>
          <v-btn color="black" class="white--text" @click="connectWallet" large>
            WalletConnect
          </v-btn>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script lang="ts">
import { connect, connector } from '@/providers/WalletConnectProvider'
import Vue from 'vue'

declare interface ComponentData {
  address: string;
  isConnected: boolean;
}

export default Vue.extend({
  name: "WalletConnect",
  data(): ComponentData {
    return {
      address: "",
      isConnected: false,
    };
  },
  mounted() {
    connect()
    
    if (connector) {
      this.isConnected = connector.connected
      this.address = connector.accounts[0]
      this.subscribeToEvents();
    }
  },
  methods: {
    async disconnect() {
      await connector.killSession();
      this.isConnected = connector.connected;
    },
    async connectWallet() {
      connect()
      await connector.createSession();
      this.subscribeToEvents();
    },
    subscribeToEvents() {
      connector.on("connect", (error, payload) => {
        if (error) {
          throw error;
        }

        const { params } = payload;
        const { accounts } = params[0];

        this.isConnected = true;
        this.address = accounts[0];
      });
      connector.on("disconnect", (error) => {
        if (error) {
          throw error;
        }

        this.isConnected = false;
      });
    },
  },
});
</script>