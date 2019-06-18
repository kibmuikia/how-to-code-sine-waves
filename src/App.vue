<template>
  <v-app>
    <Layout />
  </v-app>
</template>

<script>
export default {
  name: "App",
  components: {
    Layout: () => import("@/Layout/V1/")
  },
  data() {
    return {
      //
    };
  }
};
</script>
