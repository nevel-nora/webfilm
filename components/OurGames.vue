<template>
  <div class="our-games">
    <BaseTitle class="our-games__title title-60" :text="$t('outGames')" />
    <BaseText
      class="our-games__description montserrat-regular-14 de"
      :text="$t('asAPioneer')"
    />

    <div class="our-games__introdution">
      <div class="tw-grid tw-grid-cols-2 md:tw-grid-cols-4">
        <TheCard
          class="card tw-px-[10px]"
          v-for="(post, index) in Constants.common.listImagesCard"
          :key="index"
          :src="post.src"
          classImage="align-end white--text card-image"
          classTitle="title-card"
          classSubtitle="subtitle-card"
          :title="post.label"
          :subtitle="$t('loremIpsum')"
        />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
export default {
  name: 'OurGames',
}
</script>

<style lang="scss" scoped>
@import '@/assets/styles/components/our-games';
</style>
