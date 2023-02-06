<template>
  <div class="the-footer">
    <div class="the-footer__detail">
      <div class="the-footer__image">
        <TheImageLazy src="/images/white-logo.png" class="logo" />
        <div class="social">
          <svg-icon
            color="white"
            name="twitter"
            class="tw-h-[32px] tw-w-[26px]"
          />
          <svg-icon
            color="white"
            name="facebook"
            class="tw-h-[32px] tw-w-[26px]"
          />
          <svg-icon
            color="white"
            name="linkedin"
            class="tw-h-[32px] tw-w-[26px]"
          />
        </div>
      </div>

      <div class="the-footer__contact">
        <div>
          <BaseTitle
            class="montserrat-bold-24"
            :text="$t('footer.address.title')"
          />

          <div class="tw-flex tw-items-center tw-mb-3">
            <svg-icon
              name="address"
              class="tw-w-[30px] tw-h-[34px] tw-mr-[5px]"
            />
            <BaseText :text="$t('footer.address.list1')" />
          </div>
          <div class="tw-ml-[35px] tw-mb-4">
            <BaseText :text="$t('footer.address.list2')" />
          </div>
          <div class="tw-flex tw-items-center">
            <svg-icon
              name="phone"
              class="tw-w-[30px] tw-h-[34px] tw-mr-[5px]"
            />
            <BaseText :text="$t('footer.address.phone')" />
          </div>
        </div>

        <div>
          <BaseTitle
            class="montserrat-bold-24"
            :text="$t('footer.subscribe.title')"
          />

          <div class="tw-mb-3">{{ $t('footer.subscribe.label') }}</div>
          <BaseTextField
            color="white"
            :placeholder="$t('footer.subscribe.placeholder')"
            background-color="white"
            append-icon="mdi-arrow-right-thin"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
export default {
  name: 'TheFooter',
}
</script>

<style lang="scss" scoped>
@import '@/assets/styles/layouts/footer/the-footer';
</style>
