<template>
  <v-card class="movie-thumb">
    <v-btn
      :to="localePath(link.movie.detail)"
      class="btn-wrap"
      text
    >
      <span class="figure">
        <i class="ion-ios-play play" />
        <img :src="img" alt="text">
        <span class="figcaption">
          {{ $t('movieLanding.featured_caption') }}
        </span>
      </span>
      <span class="text">
        {{ text }}
      </span>
    </v-btn>
  </v-card>
</template>

<style lang="scss" scoped>
@use './card-style';
</style>

<script>
import link from '@/assets/text/link';
import { useLocalePath } from '#imports';

export default {
  setup() {
    const localePath = useLocalePath();
    return {
      localePath,
    };
  },
  props: {
    img: {
      type: String,
      required: true,
    },
    text: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      link,
    };
  },
};
</script>
