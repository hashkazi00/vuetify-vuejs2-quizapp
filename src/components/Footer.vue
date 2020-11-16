<template>
  <v-footer color="primary lighten-1">
    <v-row justify="center" no-gutters>
      <v-btn
        v-for="(link,key) in links"
        :key="link"
        color="white"
        text
        rounded
        href="link"
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
        BLOG: "sahilkazi.hashnode.dev",
        Github: "https://github.com/"
      }
    };
  }
};
</script>

<style>
</style>