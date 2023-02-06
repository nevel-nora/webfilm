<template>
  <div class="about">
    <div class="about-us">
      <div class="about-us__left">
        <div class="introduction">
          <BaseText :text="$t('AboutUs')" class="title-60"></BaseText>
          <BaseText
            :text="$t('browseOurSelection')"
            class="montserrat-regular-14"
          >
          </BaseText>
        </div>
        <div class="about-us__parameter">
          <div>
            <BaseText text="600m+" class="montserrat-bold-80"></BaseText>
            <BaseText :text="$t('users')" class="montserrat-bold-24"></BaseText>
          </div>
          <div>
            <BaseText text="135+" class="montserrat-bold-80"></BaseText>
            <BaseText :text="$t('games')" class="montserrat-bold-24"></BaseText>
          </div>
        </div>
      </div>
      <div class="about-us__right">
        <div class="introduction">
          <svg-icon name="canlender" />
          <div>
            <BaseText
              :text="$t('24Hour')"
              class="montserrat-bold-24"
            ></BaseText>
            <BaseText :text="$t('24/7')" class="montserrat-regular-24">
            </BaseText>
          </div>
        </div>
        <div class="introduction">
          <svg-icon name="design" />
          <div>
            <BaseText
              :text="$t('design')"
              class="montserrat-bold-24"
            ></BaseText>
            <BaseText :text="$t('combining')" class="montserrat-regular-24">
            </BaseText>
          </div>
        </div>
        <div class="introduction">
          <svg-icon name="team" />
          <div>
            <BaseText :text="$t('team')" class="montserrat-bold-24"></BaseText>
            <BaseText :text="$t('etechIsAn')" class="montserrat-regular-24">
            </BaseText>
          </div>
        </div>
      </div>
    </div>
    <div class="about-image-animation">
      <The-Image-Lazy id="illustrator" src="/images/Illustrator.png" />
      <The-Image-Lazy id="map" src="/images/Pin-map.png" />
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({})
</script>

<style lang="scss" scoped>
@import '@/assets/styles/components/about-us';
</style>
