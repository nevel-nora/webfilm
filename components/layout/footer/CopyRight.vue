<template>
  <div class="copyright montserrat-regular-18">
    <BaseText :text="$t('footer.copyright.title')" />
  </div>
</template>

<script lang="ts">
export default {
  name: 'CopyRight',
}
</script>

<style lang="scss" scoped>
@import '@/assets/styles/layouts/footer/copyright';
</style>
