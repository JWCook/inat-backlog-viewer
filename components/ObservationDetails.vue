<template>
  <div>
    <v-card-title>
      <div class="card-title">
        <b>{{ observation.taxon_rank }}:&nbsp;</b>
        <a
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
        <v-btn class="ma-2" color="green lighten-2" text>View on iNaturalist</v-btn>
      </a>
      <v-spacer></v-spacer>
      <v-btn icon><v-icon>mdi-bookmark</v-icon></v-btn>
    </v-card-actions>
  </div>
</template>

<script>
export default {
  name: 'ObservationDetails',
  props: {
    observation: Object,
  },
};
</script>

<style>
.card-title {
  white-space: nowrap;
  word-break: normal;
  overflow: hidden;
  text-overflow: ellipsis;
}
</style>
