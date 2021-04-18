<template>
  <div>
    <Gallery />
    <ObservationPhoto />
  </div>
</template>

<script>
import Gallery from '@/components/Gallery.vue';
import ObservationPhoto from '~/components/ObservationPhoto.vue';
export default {
  name: 'Photo',
  components: {
    Gallery,
    ObservationPhoto,
  },
};
</script>
