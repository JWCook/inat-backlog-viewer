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
            <nuxt-link
              :to="{ name: 'photo-id', params: { id: observation.id, observation: observation } }"
            >
              <v-hover v-slot="{ hover }">
                <v-img :src="observation.photo_medium_url" aspect-ratio="1" class="grey lighten-2">
                  <template #placeholder>
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
                        <ul style="list-style-type: none; padding-left: 0;">
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
                      </p>
                      <b>Ranking values:</b>
                      <ul>
                        <li v-for="(value, key) in observation.ranking_values" :key="key">
                          <b>{{ key }}:</b> {{ value }}
                        </li>
                      </ul>
                    </div>
                  </v-expand-transition>
                </v-img>
              </v-hover>
            </nuxt-link>

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
  </div>
</template>

<script>
import observations from '~/assets/observations.json'
export default {
  name: 'Observation',
  data() {
    return {
      observations,
    }
  },
}
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
.card-title {
  white-space: nowrap;
  word-break: normal;
  overflow: hidden;
  text-overflow: ellipsis;
}
</style>
