<template>
  <div>
    <CoolLightBox
      :items="observations"
      :index="index"
      :full-screen="true"
      :slideshow="false"
      :use-zoom-bar="true"
      src-name="photo_original_url"
      src-thumb="photo_medium_url"
      thumbs-position="bottom"
      @close="index = null"
    >
    </CoolLightBox>
    <v-container class="images-wrapper">
      <v-row>
        <v-spacer></v-spacer>
        <v-col
          v-for="(observation, obsIndex) in observations"
          :key="observation.id"
          class="d-flex child-flex"
          xs="12"
          sm="12"
          md="6"
          lg="4"
          xl="3"
        >
          <v-card class="pa-2 mx-1 my-2">
            <v-hover v-slot="{ hover }">
              <v-img
                :src="observation.photo_medium_url"
                aspect-ratio="1"
                class="grey lighten-2 image"
                @click="index = obsIndex"
              >
                <template #placeholder>
                  <v-row class="fill-height ma-0" align="center" justify="center">
                    <v-progress-circular indeterminate color="grey lighten-5"></v-progress-circular>
                  </v-row>
                </template>

                <!-- Hover overlay -->
                <v-expand-transition>
                  <div
                    v-if="hover"
                    class="transition-fast-in-fast-out grey darken-2 v-card--reveal white--text"
                    style="height: 100%"
                  >
                    <ul style="list-style-type: none; padding-left: 0">
                      <li>
                        <b>IDs:</b>
                        {{ observation.num_identification_agreements }} agreements,
                        {{ observation.num_identification_disagreements }} disagreements
                      </li>
                      <li><b>Created at:</b> {{ observation.created_at }}</li>
                      <li><b>Updated at:</b> {{ observation.updated_at }}</li>
                      <li v-if="observation.short_description">
                        <b>Description:</b> {{ observation.short_description }}
                      </li>
                    </ul>
                    <br /><b>Ranking values:</b>
                    <ul>
                      <li v-for="(value, key) in observation.ranking_values" :key="key">
                        <b>{{ key }}:</b> {{ value }}
                      </li>
                    </ul>
                  </div>
                </v-expand-transition>
              </v-img>
            </v-hover>

            <!-- Card info + buttons -->
            <ObservationDetails :observation="observation" />
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import 'vue-cool-lightbox/dist/vue-cool-lightbox.min.css';
import CoolLightBox from 'vue-cool-lightbox';
import ObservationDetails from '~/components/ObservationDetails.vue';
import observations from '~/assets/observations.json';

export default {
  name: 'GalleryItem',
  components: {
    CoolLightBox,
    ObservationDetails,
  },
  data() {
    return {
      index: null,
      observations,
    };
  },
};
</script>

<style>
.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(20rem, 1fr));
  grid-gap: 1rem;
  max-width: 80rem;
  margin: 5rem auto;
  padding: 0 5rem;
}
.gallery-panel img {
  width: 100%;
  height: 22vw;
  object-fit: cover;
  border-radius: 0.75rem;
}
.v-card--reveal {
  align-items: left;
  bottom: 0;
  justify-content: left;
  opacity: 0.8;
  position: absolute;
  width: 100%;
}
</style>
