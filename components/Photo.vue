<template>
  <div class="lighbox">
    <v-overlay :value="overlay">
      <v-container>
        <v-row>
          <v-spacer></v-spacer>
          <v-col class="d-flex child-flex" cols="12">
            <v-card class="pa-2 ma-2" v-click-outside="closeLightbox">
              <!-- Image + placeholder -->
              <v-img
                :src="observation.photo_original_url"
                contain
                max-height="80vh"
                max-width="50vw"
              >
                <template v-slot:placeholder>
                  <v-row
                    class="fill-height ma-0"
                    align="center"
                    justify="center"
                  >
                    <v-progress-circular
                      indeterminate
                      color="grey lighten-5"
                    ></v-progress-circular>
                  </v-row>
                </template>
              </v-img>

              <!-- Card info -->
              <v-card-title>{{
                observation.taxon_formatted_name
              }}</v-card-title>
              <!-- <p v-if="observation.title">{{ observation.title }}</p> -->
              <!-- <p v-if="observation.location">{{ observation.location }}</p> -->
              <!-- <p v-if="observation.photographer">
                <a rel="nofollow" :href="observation.photographer.url">{{ observation.photographer.name }}</a>
              </p> -->
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-overlay>
  </div>
</template>

<script>
import observations from '~/assets/observations.json'
export default {
  name: 'Photo',
  data() {
    return {
      observations,
      overlay: true,
    }
  },
  computed: {
    observation() {
      return this.observations.find((observation) => {
        return observation.id === Number(this.$route.params.id)
      })
    },
  },
  methods: {
    closeLightbox() {
      this.overlay = false
      this.$router.push('/')
    },
  },
}
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
