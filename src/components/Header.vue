<template>
  <v-app-bar color="primary" dark dense>
    <h1 class="display-0">Quiz Hub</h1>
    <v-spacer></v-spacer>
    <p class="ma-0">Counter: {{ numCorrect }}/{{ numTotal }}</p>
  </v-app-bar>
</template>

<script>
export default {
  name: "Header",
  props: {
    numCorrect: Number,
    numTotal: Number,
  },
};
</script>
