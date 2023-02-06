<template>
  <v-text-field
    outlined
    hide-details="auto"
    dense
    v-bind="$attrs"
    class="base-text-field"
    v-on="$listeners"
  />
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'BaseTextField',
})
</script>

<style lang="scss" scoped>
@import '@/assets/styles/components/base-text-field';
</style>
