<template>
  <div class="lighbox">
    <v-overlay :value="overlay">
      <v-container>
        <v-row>
          <v-spacer></v-spacer>
          <v-col class="d-flex child-flex" cols="12">
            <v-card class="pa-2 ma-2" v-click-outside="closeLightbox">
              <!-- Image + placeholder -->
              <v-img :src="photoUrl(photo.filename)" contain max-height="80vh" max-width="50vw">
                <template v-slot:placeholder>
                  <v-row class="fill-height ma-0" align="center" justify="center">
                    <v-progress-circular indeterminate color="grey lighten-5"></v-progress-circular>
                  </v-row>
                </template>
              </v-img>

              <!-- Card info -->
              <v-card-title>{{ photo.filename }}</v-card-title>
              <p v-if="photo.title">{{ photo.title }}</p>
              <p v-if="photo.location">{{ photo.location }}</p>
              <p v-if="photo.photographer">
                <a rel="nofollow" :href="photo.photographer.url">{{ photo.photographer.name }}</a>
              </p>
              <p v-if="photo.source">
                via
                <a rel="nofollow" :href="photo.source.url">{{ photo.source.name }}</a>
              </p>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-overlay>
  </div>
</template>

<script>
import photos from "@/photos.json";
export default {
  name: "Photo",
  data() {
    return {
      photos,
      overlay: true,
    };
  },
  computed: {
    photo() {
      return this.photos.find((photo) => {
        return photo.id === Number(this.$route.params.id);
      });
    },
  },
  methods: {
    photoUrl(filename) {
      return require(`../assets/images/${filename}`);
    },
    thumbUrl(filename) {
      return require(`../assets/images/thumbnails/${filename}`);
    },
    closeLightbox() {
      this.overlay = false;
      this.$router.push("/");
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
