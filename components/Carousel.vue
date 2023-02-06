<template>
  <div class="carousel">
    <BaseText :text="$t('ourPartners')" class="title-80"></BaseText>
    <v-sheet>
      <v-slide-group mandatory show-arrows>
        <v-slide-item v-for="(image, index) in listImages" :key="index">
          <img
            width="260"
            height="100"
            class="px-2"
            :src="`/images/${image}.png`"
          />
        </v-slide-item>
        <template v-slot:prev>
          <v-btn large elevation="2" icon>
            <v-icon> mdi-chevron-left </v-icon>
          </v-btn>
        </template>
        <template v-slot:next>
          <v-btn large elevation="2" icon>
            <v-icon> mdi-chevron-right </v-icon>
          </v-btn>
        </template>
      </v-slide-group>
    </v-sheet>
  </div>
</template>

<script lang="ts">
interface IDataProps {
  listImages: String[]
}

export default {
  data(): IDataProps {
    return {
      listImages: [
        'Rectangle57',
        'Rectangle58',
        'Rectangle59',
        'Rectangle60',
        'Rectangle61',
        'Rectangle62',
        'Rectangle63',
      ],
    }
  },
}
</script>

<style lang="scss" scoped>
@import '@/assets/styles/components/carousel';
</style>
