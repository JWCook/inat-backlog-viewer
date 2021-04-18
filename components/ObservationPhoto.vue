<template>
  <div class="lighbox">
    <v-overlay :value="overlay">
      <v-container>
        <v-row>
          <v-spacer></v-spacer>
          <v-col class="d-flex child-flex" cols="12">
            <v-card v-click-outside="closeLightbox" class="pa-2 ma-2">
              <!-- Image + placeholder -->
              <v-img
                :src="observation.photo_original_url"
                contain
                max-height="80vh"
                max-width="50vw"
              >
                <template #placeholder>
                  <v-row class="fill-height ma-0" align="center" justify="center">
                    <v-progress-circular indeterminate color="grey lighten-5"></v-progress-circular>
                  </v-row>
                </template>
              </v-img>

              <!-- Card info + buttons -->
              <v-card-title>
                <div class="card-title">
                  <b>{{ observation.taxon_rank }}:&nbsp;</b>
                  <br /><a
                    :href="'https://www.inaturalist.org/taxa/' + observation.taxon_id"
                    :title="observation.taxon_formatted_name"
                  >
                    {{ observation.taxon_formatted_name }}
                  </a>
                </div>
              </v-card-title>
              <v-card-text>
                <b>Observed by:</b>
                <a :href="'https://www.inaturalist.org/people/' + observation.user_id">
                  {{ observation.user_login }}
                </a>
                on {{ observation.observed_on }}
              </v-card-text>
              <v-card-actions>
                <a :href="'https://www.inaturalist.org/observations/' + observation.id">
                  <v-btn color="green lighten-2" text>Details on iNaturalist</v-btn>
                </a>
                <v-spacer></v-spacer>
                <v-btn icon><v-icon>mdi-bookmark</v-icon></v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-overlay>
  </div>
</template>

<script>
import observations from '~/assets/observations.json';
export default {
  name: 'Photo',
  data() {
    return {
      observations,
      overlay: true,
    };
  },
  computed: {
    observation() {
      return this.$route.params.observation;
    },
  },
  methods: {
    closeLightbox() {
      this.overlay = false;
      this.$router.push('/');
    },
  },
};
</script>

<style>
.lightbox {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  /* background-color: rgba(0, 0, 0, 0.8); */
  /* display: grid; */
  /* grid-template-columns: repeat(3, 1fr); */
  /* grid-gap: 2rem; */
}
</style>
