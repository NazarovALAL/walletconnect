<template>
  <v-app-bar app color="black" dark>
    <div class="d-flex align-center">
      <v-img
        alt="GMT Logo"
        class="shrink mr-2"
        contain
        src="@/assets/logo.svg"
        transition="scale-transition"
        width="80"
      />
    </div>

    <v-spacer></v-spacer>

    <v-btn href="https://gmt.io/en" target="_blank" text>
      <span class="mr-2">Our site</span>
      <v-icon>mdi-open-in-new</v-icon>
    </v-btn>
  </v-app-bar>
</template>