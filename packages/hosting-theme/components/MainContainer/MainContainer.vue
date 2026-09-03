<template>
  <div class="main-wrap">
    <main-header :invert="invert"/>
    <div class="container-wrap" :class="{ 'scroll-nav-content' : navScroll }">
      <slot />
    </div>
    <main-footer v-if="invert" invert />
    <footer-with-counter v-else />
  </div>
</template>

<style lang="scss" scoped>
@function section-margin($margin) {
  @return $margin * 20;
}

.main-wrap {
  position: relative;
  width: 100%;
  overflow: hidden;
  @include palette-text-primary;
  .v-theme--dark & {
    background-color: $dark-background-default;
  }
  .v-theme--light & {
    background-color: $light-background-paper;
  }
}

.space-top {
  margin-top: section-margin($spacing1);
}
</style>

<script setup>
import MainHeader from '@/components/Header';
import FooterWithCounter from '@/components/Footer/FooterWithCounter';
import MainFooter from '@/components/Footer';

const { invert, navScroll } = defineProps({
  invert: {
    type: Boolean,
    default: false,
  },
  navScroll: {
    type: Boolean,
    default: false,
  }
});
</script>