<template>
  <p v-bind="$attrs" class="base-text">
    {{ text }}
  </p>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'BaseText',

  props: {
    text: {
      type: String || Number,
      default: '',
    },
  },
})
</script>
