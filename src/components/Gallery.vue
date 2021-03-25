<template>
  <div>
    <v-container>
      <v-row>
        <v-spacer></v-spacer>
        <v-col
          v-for="observation in observations"
          :key="observation.id"
          class="d-flex child-flex"
          xs="12"
          sm="12"
          md="6"
          lg="4"
          xl="3"
        >
          <v-card class="pa-2 mx-1 my-2">
            <!-- Image + placeholder -->
            <router-link :to="`/photo/${observation.id}`">
              <v-hover v-slot="{ hover }">
                <v-img :src="observation.photo_medium_url" aspect-ratio="1" class="grey lighten-2">
                  <template v-slot:placeholder>
                    <v-row class="fill-height ma-0" align="center" justify="center">
                      <v-progress-circular
                        indeterminate
                        color="grey lighten-5"
                      ></v-progress-circular>
                    </v-row>
                  </template>

                  <!-- Hover overlay -->
                  <v-expand-transition>
                    <div
                      v-if="hover"
                      class="transition-fast-in-fast-out grey darken-2 v-card--reveal white--text"
                      style="height: 100%"
                    >
                      <p>
                        <b>IDs:</b> {{ observation.num_identification_agreements }} agreements,
                        {{ observation.num_identification_disagreements }} disagreements
                      </p>
                      <p>
                        <b>Created at:</b> {{ observation.created_at }}<br />
                        <b>Updated at:</b> {{ observation.updated_at }}
                      </p>
                      <!-- <br /><b>Ranking values:</b> -->
                      <!-- {% for k, v in observation.ranking_values.items() %}
                      {{ '<br />&emsp;<b>' + k + ':</b> ' + v }} {% endfor %} -->
                      <p v-if="observation.description">
                        <b>Description:</b> {{ observation.description }}}
                      </p>
                    </div>
                  </v-expand-transition>
                </v-img>
              </v-hover>
            </router-link>

            <!-- Card info + buttons -->
            <v-card-title>
              <b>{{ observation.taxon_rank }}:</b> {{ observation.taxon_formatted_name }}
            </v-card-title>
            <v-card-text>This is some text</v-card-text>
            <v-card-actions>
              <v-btn color="green lighten-2" text>Details</v-btn>
              <v-spacer></v-spacer>
              <v-btn icon><v-icon>mdi-heart</v-icon></v-btn>
              <v-btn icon><v-icon>mdi-bookmark</v-icon></v-btn>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import observations from '@/observations.json';
export default {
  name: 'Observation',
  data() {
    return {
      observations,
      overlay: true,
    };
  },
  methods: {
    thumbUrl(filename) {
      return require(`../assets/images/thumbnails/${filename}`);
    },
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
