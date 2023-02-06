<template>
  <v-app light class="tw-bg-[#1d1d1d]">
    <Header />
    <nuxt />
    <!-- <TheFooter />
    <CopyRight /> -->
  </v-app>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'DefaultLayout',
})
</script>
