<template>
  <div :class="cssClasses">
    <slot />
  </div>
</template>

<script lang="ts">
import { createComponent } from '@vue/composition-api'

export default createComponent({
  name: 'VcContainer',
  props: {
    fluid: {
      type: Boolean,
      default: false,
    },
  },
  computed: {
    cssClasses() {
      return this.fluid ? 'vc-container--fluid' : 'vc-container'
    },
  },
})
</script>

<style lang="scss">
@import "../../../styles/mixins/breakpoints";
// Container mixins

@mixin make-container($padding-x: $container-padding-x) {
  width: 100%;
  padding-right: $padding-x;
  padding-left: $padding-x;
  margin-right: auto;
  margin-left: auto;
}

// For each breakpoint, define the maximum width of the container in a media query
@mixin make-container-max-widths($max-widths: $container-max-widths, $breakpoints: $grid-breakpoints) {
  @each $breakpoint, $container-max-width in $max-widths {
    @include media-breakpoint-up($breakpoint, $breakpoints) {
      max-width: $container-max-width;
    }
  }
}

.vc-container {
  @include make-container();
  @include make-container-max-widths();
}

// 100% wide container at all breakpoints
.vc-container--fluid {
  @include make-container();
}
</style>
