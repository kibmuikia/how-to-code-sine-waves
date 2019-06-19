<template>
  <v-container app fluid class="grey lighten-3">
    <!-- . -->
    <v-toolbar app fixed>
      <v-toolbar-title>Kib Waves</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-toolbar-items class="hidden-sm-and-down">
        <v-btn
          v-for="(link, index) in links"
          :key="index"
          icon
          flat
          :to="link.path"
        >
          <v-icon>{{ link.icon }}</v-icon>
        </v-btn>
      </v-toolbar-items>
      <v-toolbar-side-icon @click.stop="drawer = !drawer"></v-toolbar-side-icon>
    </v-toolbar>
    <!-- . -->
    <v-navigation-drawer temporary fixed v-model="drawer" app>
      <v-toolbar flat>
        <v-list>
          <v-list-tile>
            <v-list-tile-title class="title">
              Kib Waves
            </v-list-tile-title>
            <v-list-tile-content>
              <v-btn icon small flat color="warning" @click="drawer = false">
                <v-icon>close</v-icon>
              </v-btn>
            </v-list-tile-content>
          </v-list-tile>
        </v-list>
      </v-toolbar>

      <v-divider></v-divider>

      <v-list dense class="pt-0">
        <v-list-tile
          v-for="(link, index) in links"
          :key="index"
          :to="link.path"
        >
          <v-list-tile-action>
            <v-icon>{{ link.icon }}</v-icon>
          </v-list-tile-action>

          <v-list-tile-content>
            <v-list-tile-title>{{ link.title }}</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    <!-- . -->
    <v-content>
      <router-view></router-view>
    </v-content>
    <!-- . -->
    <v-footer height="auto" class="" app>
      <v-card class="flex grey lighten-2 elevation-15" flat tile>
        <v-card-text>
          <v-layout row wrap align-center justify-space-around>
            <v-flex xs12 md5>
              <p class="subheading">
                Get connected with me on social networks!
              </p>
            </v-flex>
            <v-flex xs12 md5 class="">
              <v-btn
                class="mx-2 info right"
                icon
                href="https://www.instagram.com/kibmuikia/"
                target="_blank"
              >
                <font-awesome-icon
                  :icon="{ prefix: 'fab', iconName: 'instagram' }"
                />
              </v-btn>
              <v-btn
                class="mx-2 info right"
                icon
                href="https://twitter.com/MuikiaAllan"
                target="_blank"
              >
                <font-awesome-icon
                  :icon="{ prefix: 'fab', iconName: 'twitter' }"
                />
              </v-btn>
            </v-flex>
          </v-layout>
        </v-card-text>

        <v-card-actions class="justify-center">
          <p>&copy;{{ currentyear }} — Developed by Muikia Allan</p>
        </v-card-actions>
      </v-card>
    </v-footer>
    <!-- . -->
  </v-container>
</template>

<script>
/* eslint-disable no-console */
/* eslint-disable no-unused-vars */

let SELF;

export default {
  name: "layout-v1",
  components: {},
  props: {},
  data() {
    return {
      drawer: null,
      links: [
        { title: "Home", icon: "home", path: "/" }
        // { title: "About", icon: "question_answer", path: "/about" }
      ],
      currentyear: new Date().getFullYear()
    };
  },
  methods: {
    // .
  },
  computed: {},
  watch: {},
  beforeCreate() {
    SELF = this;
  },
  created() {},
  mounted() {}
};
</script>

<style scoped>
/*.*/
</style>
