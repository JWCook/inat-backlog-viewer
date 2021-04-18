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
              <ObservationDetails :observation="observation" />
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-overlay>
  </div>
</template>

<script>
import ObservationDetails from '~/components/ObservationDetails.vue';
export default {
  name: 'Photo',
  components: {
    ObservationDetails,
  },
  data() {
    return {
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
