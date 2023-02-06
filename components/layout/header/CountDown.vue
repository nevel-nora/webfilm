<template>
  <div class="count-down">
    <h1 class="count-down__title title-80">
      {{ $t('weAreGettingReady') }}
    </h1>
    <div class="count-down__area">
      <div class="count-down__area--first">
        <div>
          <BaseText :text="new Date().getDate()" />
          <BaseText :text="$t('Days')" />
        </div>
        <span>:</span>
        <div>
          <BaseText :text="new Date().getHours()" />
          <BaseText :text="$t('Hours')" />
        </div>
        <span>:</span>
        <div>
          <BaseText :text="new Date().getMinutes()" />
          <BaseText :text="$t('Minutes')" />
        </div>
        <span>:</span>
        <div>
          <BaseText :text="new Date().getSeconds()" />
          <BaseText :text="$t('Second')" />
        </div>
      </div>
      <div class="count-down__area--center">
        <BaseText :text="$t('weWillBack')" />
      </div>
      <div class="count-down__area--last">
        <BaseTextField
          color="white"
          :placeholder="$t('enterYourEmail')"
          background-color="white"
          append-icon="mdi-arrow-right-thin"
        />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({})
</script>
<style lang="scss" scoped>
@import '@/assets/styles/layouts/header/countdown';
</style>
