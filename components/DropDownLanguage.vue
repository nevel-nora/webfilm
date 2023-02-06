<template>
  <v-menu offset-y left>
    <template v-slot:activator="{ on, attrs }">
      <v-btn text :outlined="outlined" v-bind="attrs" v-on="on">
        <The-Image-Lazy :src="`/images/${$i18n.locale}.png`" />
        <svg-icon id="svg-down" :name="outlined ? 'down-black' : 'down'" />
      </v-btn>
    </template>
    <v-list>
      <div
        v-for="(locale, index) in $i18n.locales"
        :key="index"
        class="drop-down"
      >
        <div class="drop-down__item" @click="onChange(locale.code)">
          <div>
            <svg-icon
              v-show="$i18n.locale === locale.code"
              id="check-box"
              name="checkBox"
            />
          </div>
          <img :src="`/images/${locale.code}.png`" loading="lazy" />
          <p class="montserrat-bold-10">{{ locale.name }}</p>
        </div>
      </div>
    </v-list>
  </v-menu>
</template>
<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  props: {
    outlined: Boolean,
  },
  methods: {
    onChange(event: string) {
      console.log('here')
      this.$emit('closeMenu')

      // setTimeout(() => {
      this.$router.replace(this.switchLocalePath(event))
      // }, 1000)
    },
  },
})
</script>
<style lang="scss" scoped>
@import '@/assets/styles/components/drop-down-language';
</style>
