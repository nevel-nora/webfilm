<template>
  <nav class="tw-bg-[#1d1d1d] tw-border tw-border-[#2f2f2f] tw-text-[#919191]">
    <div class="tw-mx-auto tw-max-w-7xl tw-px-2 sm:tw-px-6 lg:tw-px-8">
      <div
        class="tw-relative tw-flex tw-h-16 tw-items-center tw-justify-between"
      >
        <div
          class="tw-absolute tw-inset-y-0 tw-left-0 tw-flex tw-items-center sm:tw-hidden"
        >
          <button
            type="button"
            class="tw-inline-flex tw-items-center tw-justify-center tw-rounded-md tw-p-2 tw-text-gray-400 hover:tw-bg-gray-700 hover:tw-text-white focus:tw-outline-none focus:tw-ring-2 focus:tw-ring-inset focus:tw-ring-white"
            aria-controls="mobile-menu"
            aria-expanded="false"
          >
            <span class="tw-sr-only">Open main menu</span>

            <svg
              class="tw-block tw-h-6 tw-w-6"
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
              aria-hidden="true"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25h16.5"
              />
            </svg>

            <svg
              class="tw-hidden tw-h-6 tw-w-6"
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
              aria-hidden="true"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M6 18L18 6M6 6l12 12"
              />
            </svg>
          </button>
        </div>
        <div
          class="tw-flex tw-flex-1 tw-items-center tw-justify-center sm:tw-items-stretch sm:tw-justify-start"
        >
          <div class="tw-flex tw-flex-shrink-0 tw-items-center">
            <img
              class="tw-block tw-h-8 tw-w-auto lg:tw-hidden"
              src="https://tailwindui.com/img/logos/mark.svg?color=indigo&shade=500"
              alt="Your Company"
            />
            <img
              class="tw-hidden tw-h-8 tw-w-auto lg:tw-block"
              src="https://tailwindui.com/img/logos/mark.svg?color=indigo&shade=500"
              alt="Your Company"
            />
          </div>
          <div class="tw-hidden sm:tw-ml-6 sm:tw-block">
            <div class="tw-flex tw-space-x-4">
              <a
                href="#"
                class="tw-text-purple-900 tw-px-3 tw-py-2 tw-rounded-md tw-text-sm tw-font-medium"
                aria-current="page"
                >Home</a
              >

              <a
                href="#"
                class="tw-text-[#919191] hover:tw-bg-gray-700 hover:tw-text-white tw-px-3 tw-py-2 tw-rounded-md tw-text-sm tw-font-medium"
                >4K</a
              >

              <a
                href="#"
                class="tw-text-[#919191] hover:tw-bg-gray-700 hover:tw-text-white tw-px-3 tw-py-2 tw-rounded-md tw-text-sm tw-font-medium"
                >Trending</a
              >

              <a
                href="#"
                class="tw-text-[#919191] hover:tw-bg-gray-700 hover:tw-text-white tw-px-3 tw-py-2 tw-rounded-md tw-text-sm tw-font-medium"
              >
                Browse Movies</a
              >
            </div>
          </div>
        </div>
        <div
          class="tw-absolute tw-inset-y-0 tw-right-0 tw-flex tw-items-center tw-pr-2 sm:tw-static sm:tw-inset-auto sm:tw-ml-6 sm:tw-pr-0"
        >
          <button
            type="button"
            class="tw-rounded-full tw-bg-gray-800 tw-p-1 tw-text-gray-400 hover:tw-text-white focus:tw-outline-none focus:tw-ring-2 focus:tw-ring-white focus:tw-ring-offset-2 focus:tw-ring-offset-gray-800"
          >
            <span class="tw-sr-only">View notifications</span>
            <svg
              class="tw-h-6 tw-w-6"
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
              aria-hidden="true"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M14.857 17.082a23.848 23.848 0 005.454-1.31A8.967 8.967 0 0118 9.75v-.7V9A6 6 0 006 9v.75a8.967 8.967 0 01-2.312 6.022c1.733.64 3.56 1.085 5.455 1.31m5.714 0a24.255 24.255 0 01-5.714 0m5.714 0a3 3 0 11-5.714 0"
              />
            </svg>
          </button>

          <div class="tw-relative tw-ml-3">
            <div>
              <button
                type="button"
                class="tw-flex tw-rounded-full tw-bg-gray-800 tw-text-sm focus:tw-outline-none focus:tw-ring-2 focus:tw-ring-white focus:tw-ring-offset-2 focus:tw-ring-offset-gray-800"
                id="user-menu-button"
                aria-expanded="false"
                aria-haspopup="true"
              >
                <span class="tw-sr-only">Open user menu</span>
                <img
                  class="tw-h-8 tw-w-8 tw-rounded-full"
                  src="https://img.freepik.com/free-vector/cute-angry-cat-dino-destroy-building-cartoon-vector-icon-illustration-animal-holiday-icon-isolated_138676-6767.jpg?w=740&t=st=1673855357~exp=1673855957~hmac=52bace383968bc043f2772b3e57d8d43a0164e821ad0d7d997d7f84e542399a7"
                  alt=""
                />
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<script lang="ts">
import Vue from 'vue'
interface IDataProps {
  moveUp: boolean
  startY: number
}
export default Vue.extend({
  name: 'Header',

  data(): IDataProps {
    return {
      moveUp: true,
      startY: 0,
    }
  },

  methods: {
    handleScroll() {
      var scrollY = window.scrollY
      if (scrollY > this.startY) {
        this.moveUp = false
      } else {
        this.moveUp = true
      }
      this.startY = scrollY
    },

    onScroll() {
      window.scrollTo(0, !this.moveUp ? 0 : document.body.scrollHeight)
    },
  },
  mounted: function () {
    window.addEventListener('scroll', this.handleScroll)
  },
  destroyed: function () {
    window.removeEventListener('scroll', this.handleScroll)
  },
})
</script>

<style lang="scss" scoped>
@import '@/assets/styles/layouts/header/index';
</style>
