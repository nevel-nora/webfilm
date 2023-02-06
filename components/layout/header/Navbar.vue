<template>
  <div>
    <DropDownNavbar
      :navbars="navbars"
      @closeMenu="isOpenNavbarMenu = false"
      v-show="isOpenNavbarMenu"
    />

    <div class="navbar">
      <img class="navbar__logo" src="/images/white-logo.png" />
      <div class="navbar__redirect">
        <nuxt-link
          class="montserrat-bold-14 uppercase"
          v-for="(navbar, index) in navbars"
          :key="index"
          :to="navbar.link"
        >
          {{ navbar.label }}
        </nuxt-link>
        <DropDownLanguage />
      </div>
    </div>

    <v-btn
      text
      v-show="!isOpenNavbarMenu"
      @click="isOpenNavbarMenu = !isOpenNavbarMenu"
    >
      <svg-icon id="menu" name="menu" />
    </v-btn>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { INavbars } from '~/models/header'
interface IDataProps {
  navbars: INavbars[]
  isOpenNavbarMenu: boolean
}
export default Vue.extend({
  name: 'Navbar',

  data(): IDataProps {
    return {
      navbars: [
        {
          label: this.$t('aboutUs').toString(),
          link: '#',
        },
        {
          label: this.$t('games').toString(),
          link: '#',
        },
        {
          label: this.$t('partners').toString(),
          link: '#',
        },
        {
          label: this.$t('contactUs').toString(),
          link: '#',
        },
      ],
      isOpenNavbarMenu: false,
    }
  },

  methods: {
    closeMenu() {
      console.log('this.isOpenNavbarMenu------------------------')
    },
  },

  watch: {
    isOpenNavbarMenu(): void {
      document.querySelectorAll('html')[0].style.overflowY = this
        .isOpenNavbarMenu
        ? 'hidden'
        : 'scroll'
    },
  },
})
</script>
<style lang="scss" scoped>
@import '@/assets/styles/layouts/header/navbar';
</style>
