<template>
  <h2 v-bind="$attrs" class="base-title">
    {{ text }}
  </h2>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'BaseTitle',

  props: {
    text: {
      type: String || Number,
      default: '',
    },
  },
})
</script>
