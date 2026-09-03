<template>
  <v-btn
    :to="localePath(link.fashion.detail)"
    variant="plain"
    class="simple-thumb"
  >
    <span class="wrap">
      <span class="figure">
        <img :src="img" alt="title">
      </span>
      <span class="text">{{ title }}</span>
      <span class="price">
        <strong>{{ price }}</strong>
      </span>
    </span>
  </v-btn>
</template>

<style lang="scss" scoped>
@use './card-style.scss';
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
    title: {
      type: String,
      required: true,
    },
    price: {
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
