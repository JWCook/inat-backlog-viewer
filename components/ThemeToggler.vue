<template>
  <div>
    <v-tooltip v-if="!$vuetify.theme.dark" right open-delay="200">
      <span>Toggle dark mode on</span>
      <template #activator="{ on }">
        <v-btn color="info" small fab v-on="on" @click="toggleTheme">
          <v-icon class="mr-1">mdi-moon-waxing-crescent</v-icon>
        </v-btn>
      </template>
    </v-tooltip>

    <v-tooltip v-else right open-delay="200">
      <span>Toggle dark mode off</span>
      <template #activator="{ on }">
        <v-btn color="info" small fab v-on="on" @click="toggleTheme">
          <v-icon>mdi-white-balance-sunny</v-icon>
        </v-btn>
      </template>
    </v-tooltip>
  </div>
</template>

<script>
export default {
  data() {
    return {
      dark: this.$vuetify.theme.dark,
    };
  },
  methods: {
    toggleTheme() {
      this.$vuetify.theme.dark = !this.$vuetify.theme.dark;
    },
  },
};
</script>
