<template>
  <v-footer color="primary lighten-1">
    <v-row justify="center" no-gutters>
      <v-btn
        v-for="(link,key) in links"
        :key="key"
        :href="link"
        target="_blank"
        color="white"
        text
        rounded
        class="my-2"
      >{{ key }}</v-btn>
      <v-col class="primary lighten-2 py-4 text-center white--text" cols="12">
        {{ new Date().getFullYear() }} —
        <strong>Over Engineered with 💜</strong>
      </v-col>
    </v-row>
  </v-footer>
</template>

<script>
export default {
  name: "Footer",
  data() {
    return {
      links: {
        BLOG: "https://sahilkazi.hashnode.dev",
        Github: "https://github.com/hashkazi00",
        Portfolio: "https://www.sahilkazi.ml"
      }
    };
  }
};
</script>

<style>
</style>