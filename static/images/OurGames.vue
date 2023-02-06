<template>
  <div class="our-games">
    <div class="tw-grid tw-grid-cols-2 md:tw-grid-cols-4">
        <BasePost
          v-for="(element, index) in posts"
          :key="index"
          :src="element" 
          :class="[
            'tw-mr-[10px]',
            {
              'tw-mt-[55px]': index % 2 !== 0
            }
          ]"
        />
    </div>
  </div>
</template>

<script lang="ts">
export default {
  name: 'OurGames',

  data() {
    return {
      posts: ['/images/Bitmap.png', '/images/Bitmap2.png', '/images/Bitmap3.png', '/images/Bitmap4.png'],
    }
  },
}
</script>

<style lang="scss" scoped>
@import '@/assets/styles/components/our-games';
</style>