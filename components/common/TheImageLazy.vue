<template>
  <v-img v-bind="$attrs" :lazy-src="$attrs.src" aspect-ratio="1">
    <template v-slot:placeholder>
      <v-row class="fill-height ma-0" align="center" justify="center">
        <v-progress-circular
          indeterminate
          color="grey lighten-5"
        ></v-progress-circular>
      </v-row>
    </template>
    <slot />
  </v-img>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({})
</script>
