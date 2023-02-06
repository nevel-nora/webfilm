<template>
  <v-card v-bind="$attrs" elevation="0">
    <TheImageLazy :class="$attrs.classImage" :src="$attrs.src">
      <v-card-title :class="$attrs.classTitle">{{ $attrs.title }}</v-card-title>
      <v-card-subtitle :class="$attrs.classSubtitle">
        {{ $attrs.subtitle }}
      </v-card-subtitle>
    </TheImageLazy>
  </v-card>
</template>
<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'TheCard',
})
</script>
