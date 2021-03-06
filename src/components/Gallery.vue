<template>
  <div>
    <v-container>
      <v-row no-gutters>
        <v-col
          v-for="photo in photos"
          :key="photo.id"
          class="d-flex child-flex"
          xs="12"
          md="6"
          lg="3"
          xl="2"
          padding="0 5rem"
        >
          <v-card class="pa-2 mx-1 my-2">
            <!-- Image + placeholder -->
            <v-img
              :src="thumbUrl(photo.filename)"
              :lazy-src="`https://picsum.photos/10/6?image=${n * 5 + 10}`"
              aspect-ratio="1"
              class="grey lighten-2"
            >
              <template v-slot:placeholder>
                <v-row class="fill-height ma-0" align="center" justify="center">
                  <v-progress-circular
                    indeterminate
                    color="grey lighten-5"
                  ></v-progress-circular>
                </v-row>
              </template>
            </v-img>

            <!-- Card info + buttons -->
            <v-card-title>AAAA</v-card-title>
            <v-card-text>This is some text</v-card-text>
            <v-card-actions>
              <v-btn color="green lighten-2" text>Details</v-btn>
              <v-btn icon @click="show = !show">
                <v-icon>{{
                  show ? "mdi-chevron-up" : "mdi-chevron-down"
                }}</v-icon>
              </v-btn>
              <v-spacer></v-spacer>
              <v-btn icon><v-icon>mdi-heart</v-icon></v-btn>
              <v-btn icon><v-icon>mdi-bookmark</v-icon></v-btn>
            </v-card-actions>

            <!-- Card expansion -->
            <v-expand-transition>
              <div v-show="show">
                <v-divider></v-divider>
                <v-card-text>WHOA HEY LOOK AT THIS TEXT MAN</v-card-text>
              </div>
            </v-expand-transition>
          </v-card>
        </v-col>
      </v-row>
    </v-container>

    <h1>HI THERE</h1>

    <div class="gallery">
      <div class="gallery-panel" v-for="photo in photos" :key="photo.id">
        <router-link :to="`/photo/${photo.id}`">
          <img :src="thumbUrl(photo.filename)" />
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import photos from "@/photos.json";
export default {
  name: "Gallery",
  data() {
    return {
      photos
    };
  },
  methods: {
    thumbUrl(filename) {
      // return require(`../assets/images/thumbnails/${filename}`);
      console.log(`../assets/images/${filename}`);
      return "https://picsum.photos/200/200";
    }
  }
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
</style>
