<template>
  <div class="drop-down-navbar">
    <div class="drop-down-navbar__select">
      <DropDownLanguage @closeMenu="$emit('closeMenu')" :outlined="true" />
      <v-btn text>
        <svg-icon id="close" name="close" @click="$emit('closeMenu', false)" />
      </v-btn>
    </div>

    <div class="drop-down-navbar__button">
      <nuxt-link
        v-for="(navbar, index) in navbars"
        :key="index"
        :to="navbar.link"
      >
        {{ navbar.label }}
      </nuxt-link>
    </div>
  </div>
</template>

<script lang="ts">
import Vue, { PropType } from 'vue'
import { INavbars } from '~/models/header'

export default Vue.extend({
  props: {
    navbars: {
      type: Array as PropType<Array<INavbars>>,
      default: () => [],
    },
  },
})
</script>
<style lang="scss" scoped>
@import '@/assets/styles/layouts/header/drop-down-navbar';
</style>
