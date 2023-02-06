<template>
  <div class="tw-bg-[#1d1d1d]">
    <v-overlay :value="loading" class="tw-z-[9999]">
      <v-progress-circular indeterminate size="64"></v-progress-circular>
    </v-overlay>

    <v-overlay id="loadVideo" class="tw-z-[9999]">
      <v-progress-circular
        id="spinner"
        indeterminate
        color="green"
      ></v-progress-circular>
    </v-overlay>

    <div
      class="tw-py-[10px] tw-px-[10px] md:tw-py-[50px] md:tw-px-[120px] tw-bg-[#171717]"
    >
      <p class="tw-text-[#5a5a5a] tw-text-2xl tw-font-bold">Search Movies:</p>
      <input
        type="text"
        class="tw-w-full tw-bg-[#282828] tw-p-[10px] tw-text-white tw-rounded tw-my-[10px]"
        v-model="search"
      />
      <div
        class="tw-grid tw-grid-cols-1 sm:tw-grid-cols-3 tw-gap-[0px] sm:tw-gap-[50px]"
      >
        <div>
          <p class="tw-text-[#5a5a5a]">Quality:</p>
          <v-select
            dark
            :items="listQuality"
            v-model="quality"
            solo
            class="tw-my-[1px] sm:tw-my-[10px] tw-capitalize"
          ></v-select>
        </div>
        <div>
          <p class="tw-text-[#5a5a5a]">Genre:</p>
          <v-select
            dark
            :items="listGenre"
            v-model="genre"
            solo
            class="tw-my-[1px] sm:tw-my-[10px] tw-capitalize"
          ></v-select>
        </div>
        <div>
          <p class="tw-text-[#5a5a5a]">Order By:</p>
          <v-select
            dark
            :items="listOrderBy"
            v-model="orderBy"
            solo
            class="tw-my-[1px] sm:tw-my-[10px] tw-capitalize"
          ></v-select>
        </div>
      </div>
      <div class="tw-w-full tw-text-center">
        <button
          @click="handleSearch"
          class="tw-mx-auto tw-py-[10px] tw-px-[20px] tw-bg-[#6ac045] tw-text-white tw-rounded"
        >
          Search
        </button>
      </div>
    </div>

    <div>
      <div class="text-center tw-mt-[10px]">
        <v-pagination
          v-show="list?.length"
          v-model="page"
          :length="totalPage"
          :total-visible="7"
        ></v-pagination>
      </div>
      <div class="tw-w-[250px] md:tw-w-[600px] tw-mx-auto tw-text-center">
        <div v-if="!list?.length && !loading">
          <img
            src="https://i.pinimg.com/originals/ae/8a/c2/ae8ac2fa217d23aadcc913989fcc34a2.png"
          />
        </div>
      </div>
      <div
        class="tw-grid tw-grid-cols-2 sm:tw-grid-cols-4 tw-gap-3 lg:tw-grid-cols-6 tw-px-[10px] sm:tw-px-[100px] tw-py-[50px]"
      >
        <div
          class="tw-max-w-[175px] tw-my-4 tw-cursor-pointer tw-relative cart detail tw-mx-auto"
          v-for="(list, index) in list"
          :key="index"
          @click="handleOpenPlay(list)"
        >
          <img
            :src="list.large_cover_image"
            class="image tw-w-full tw-border-solid tw-border-[6px] tw-border-white tw-rounded"
          />
          <p
            class="tw-text-white tw-pt-2 tw-text-[16px] hover:tw-text-[#747474]"
          >
            {{ list.title }}
          </p>
          <p class="tw-text-white tw-text-[14px] hover:tw-text-[#747474]">
            {{ list.year }}
          </p>

          <div
            class="view-detail tw-absolute tw-top-[100px] tw-z-50 tw-left-0 tw-right-0 tw-mx-auto tw-text-center"
          >
            <v-icon large color="green darken-2"> mdi-star </v-icon>
            <p class="tw-text-white tw-text-[26px]">{{ list.rating }}/10</p>
            <button
              class="tw-bg-[#6ac045] tw-py-[10px] tw-px-[20px] tw-rounded tw-text-[16px] tw-text-white"
            >
              View Details
            </button>
          </div>
        </div>
      </div>

      <div class="text-center tw-my-[50px]">
        <v-pagination
          v-show="list?.length"
          v-model="page"
          :length="totalPage"
          :total-visible="7"
        ></v-pagination>
      </div>
    </div>

    <v-dialog
      v-model="dialog"
      fullscreen
      hide-overlay
      transition="dialog-bottom-transition"
    >
      <template> </template>
      <v-card class="bg-red-500" ref="test">
        <v-toolbar class="tw-bg-[#1d1d1d] tw-text-white">
          <v-btn icon dark @click="handleCloseModal">
            <v-icon>mdi-close</v-icon>
          </v-btn>
          <v-toolbar-title>{{ listDetail.title }}</v-toolbar-title>
          <v-spacer></v-spacer>
          <v-toolbar-items> </v-toolbar-items>
        </v-toolbar>
        <div
          class="tw-flex tw-px-[50px] tw-py-[50px] tw-bg-cover"
          :style="{ backgroundImage: `url(${listDetail.background_image})` }"
        >
          <div
            class="tw-max-w-[700px] tw-mx-auto tw-flex tw-flex-col sm:tw-flex-row"
          >
            <div class="tw-flex tw-flex-col sm:tw-flex-row">
              <div class="tw-w-[261px]">
                <img
                  :src="listDetail.large_cover_image"
                  class="tw-w-full tw-h-[390px] tw-border-solid tw-border-[6px] tw-border-white tw-rounded"
                />
                <button
                  class="tw-w-full tw-py-[10px] tw-border-solid tw-border-[2px] tw-border-white tw-bg-[#4b9b8e] hover:tw-bg-[#0f6355] tw-my-[10px] tw-rounded tw-font-bold"
                >
                  Download
                </button>
                <button
                  @click="initPlayer"
                  class="tw-w-full tw-py-[10px] tw-border-solid tw-border-[2px] tw-border-white tw-bg-[#6ac045] hover:tw-bg-[#467732] tw-rounded tw-font-bold"
                >
                  Watch Now
                </button>
              </div>

              <div
                class="tw-ml-[20px] tw-max-w-[250px] tw-mt-[10px] sm:tw-mt-[0px]"
              >
                <p class="tw-text-[30px] tw-pb-[10px] tw-font-bold">
                  Title: {{ listDetail.title }}
                </p>
                <p class="tw-text-[20px] tw-pb-[5px] tw-font-bold">
                  Year: {{ listDetail.year }}
                </p>
                <p class="tw-text-[18px] tw-pb-[10px] tw-font-bold">
                  Genres: {{ listDetail.genres?.toString() }}
                </p>

                <p class="tw-text-[18px] tw-pb-[10px] tw-font-bold">
                  Quality: {{ handleDisplayQuality(listDetail?.torrents) }}
                </p>
                <p class="tw-text-[18px] tw-pb-[10px] tw-font-bold">
                  Rating: {{ listDetail?.rating }}/10
                </p>
                <p class="tw-text-[18px] tw-pb-[10px] tw-font-bold">
                  Language:
                  {{ listDetail?.language?.toString()?.toUpperCase() }}
                </p>
              </div>
            </div>
            <div
              class="tw-w-[200px] tw-flex tw-flex-wrap tw-ml-[20px] tw-justify-between tw-mt-[20px] sm:tw-mt-[0px]"
            >
              <p class="tw-text-[20px] tw-font-bold">Similar Movies</p>
              <div
                class="tw-w-[95px] tw-h-[140px]"
                v-for="(item, index) in listReleted"
                @click="handleGetDetail(item.id)"
                :key="index"
              >
                <img
                  :src="item.medium_cover_image"
                  class="tw-w-full tw-border-solid tw-border-[6px] tw-border-white tw-rounded hover:tw-opacity-95 hover:tw-border-[#6ac045] tw-cursor-pointer"
                />
              </div>
            </div>
          </div>
        </div>

        <div
          class="tw-relative tw-max-w-[800px] tw-h-[400px] tw-mx-auto"
          id="ads"
          :key="reRender"
        >
          <iframe
            class="tw-relative tw-w-full tw-h-full"
            src="https://player.vimeo.com/video/795442289?h=9334e79a41background=1&autoplay=1&loop=1&byline=0&title=0&muted=1"
            title="vimeo-player"
            frameborder="0"
            webkitallowfullscreen
            mozallowfullscreen
            allowfullscreen
            allow="autoplay; fullscreen"
          ></iframe>
          <v-btn
            color="primary"
            :disabled="skipVideo"
            class="tw-absolute tw-bottom-[100px] tw-right-[80px]"
            @click="handleSkipVideo"
            >Skip Ads</v-btn
          >
        </div>

        <div>
          <div id="select" class="tw-my-2">
            <div
              class="tw-flex tw-items-center tw-font-bold tw-text-[20px] tw-ml-2"
            >
              <!-- <p>Select Quality:</p>
              <button
                v-for="(item, index) in listDetail?.torrents"
                :key="index"
                class="tw-bg-[#6ac045] tw-px-[20px] tw-py[60px] tw-rounded tw-mx-2"
                @click="initPlayer(item.hash)"
              >
                {{ item.quality + '.' + item.type.toString().toUpperCase() }}
              </button> -->
            </div>
          </div>
          <div id="player" class="webtor tw-relative"></div>
        </div>
      </v-card>
    </v-dialog>
  </div>
</template>

<script lang="ts">
import axios from 'axios'
import Vue from 'vue'
export default Vue.extend({
  name: 'IndexPage',

  data() {
    return {
      page: 1,
      movie_count: 1,
      search: '',
      list: [],
      limit: 18,
      loading: false,
      dialog: false,
      listDetail: {},
      listQuality: ['all', '480p', '1080p', '2160p', '3D'],
      quality: 'all',
      listGenre: [
        'all',
        'action',
        'adventure',
        'animation',
        'biography',
        'comedy',
        'crime',
        'documentary',
        'drama',
        'family',
      ],
      genre: 'all',
      listOrderBy: ['desc', 'asc'],
      orderBy: 'desc',
      listReleted: [],
      isLoadTorrentFinish: false,
      skipVideo: true,
      isClickSkip: false,
      reRender: 1,
    }
  },

  created() {
    if (document.getElementById('my-datatable')) return // was already loaded
    var scriptTag = document.createElement('script')
    scriptTag.src =
      'https://cdn.jsdelivr.net/npm/@webtor/embed-sdk-js/dist/index.min.js'
    scriptTag.id = 'my-datatable'

    document.getElementsByTagName('head')[0].appendChild(scriptTag)
  },
  mounted() {
    this.handleSearch()
  },

  methods: {
    onSearch() {
      this.page = 1
      this.handleSearch()
    },
    async handleSearch() {
      this.loading = true
      const { data } = await axios.get(
        `https://yts.mx/api/v2/list_movies.json?query_term=${this.search}&limit=${this.limit}&page=${this.page}&genre=${this.genre}&quality=${this.quality}&order_by=${this.orderBy}`
      )
      this.loading = false
      this.movie_count = data.data.movie_count
      this.page = data.data.page_number
      this.list = data.data.movies
    },

    async handleOpenPlay(list: any) {
      this.dialog = true
      this.listDetail = list
      await this.handleListReleted()

      this.handleAsyncData()
    },

    async handleGetDetail(id: number) {
      const player = document.getElementById('player') as any
      player.innerHTML = ''
      player.style.display = 'none'
      this.loading = true
      const { data } = await axios.get(
        `https://yts.mx/api/v2/movie_details.json?movie_id=${id}`
      )
      this.listDetail = data.data.movie
      this.handleListReleted()
      this.handleAsyncData()
      await this.$nextTick(() => {
        this.loading = false
      })
    },

    async handleListReleted() {
      this.loading = true
      const { data } = await axios.get(
        `https://yts.mx/api/v2/movie_suggestions.json?movie_id=${
          (this.listDetail as any).id
        }`
      )
      this.listReleted = data.data.movies
      this.loading = false
    },

    handleCloseModal() {
      const player = document.getElementById('player') as any
      const select = document.getElementById('select') as any
      select.style.display = 'none'
      player.innerHTML = ''
      player.style.display = 'none'
      this.dialog = false
    },

    handleAsyncData() {
      this.skipVideo = true

      this.reRender++

      const player = document.getElementById('player') as any
      player.style.display = 'none'

      const vm = this
      const windows = window as any
      windows.webtor = windows.webtor || []
      windows.webtor.push({
        id: 'player',
        width: '100%',
        height: '700px',
        magnet: `magnet:?xt=urn:btih:${
          (this.listDetail as any).torrents[0].hash
        }`,

        title: (this.listDetail as any).title_long,
        on: function (e: any) {
          if (e.name == windows.webtor.INITED) {
            player.style.display = 'none'
            // // select.style.display = 'block'
            // loadVideo.style.display = 'none'
            // player.scrollIntoView({
            //   behavior: 'smooth',
            //   block: 'start',
            //   inline: 'nearest',
            // })
            vm.isLoadTorrentFinish = true
          }

          if (e.name == windows.webtor.TORRENT_ERROR) {
            alert('Torrent error!')
          }
        },
      })
    },

    initPlayer() {
      const ads = document.getElementById('ads') as any
      ads.style.display = 'block'

      ads.scrollIntoView({
        behavior: 'smooth',
        block: 'start',
        inline: 'nearest',
      })

      setTimeout(() => {
        this.skipVideo = false
      }, 5000)
    },

    handleSkipVideo() {
      if (!this.isLoadTorrentFinish) {
        this.isClickSkip = true
        const loadVideo = document.getElementById('loadVideo') as any
        loadVideo.style.display = 'block'
      } else {
        const ads = document.getElementById('ads') as any
        ads.style.display = 'none'
        this.handleShownVideo()
      }
    },

    handleShownVideo() {
      const player = document.getElementById('player') as any
      const select = document.getElementById('select') as any
      select.style.display = 'block'
      player.style.display = 'block'
      player.scrollIntoView({
        behavior: 'smooth',
        block: 'start',
        inline: 'nearest',
      })
    },

    // async initPlayer(quality?: any) {
    //   const player = document.getElementById('player') as any
    //   const select = document.getElementById('select') as any
    //   const loadVideo = document.getElementById('loadVideo') as any

    //   loadVideo.style.display = 'block'

    //   player.innerHTML = ''
    //   player.style.display = 'none'
    //   select.style.display = 'none'

    //   const vm = this

    //   const windows = window as any
    //   windows.webtor = windows.webtor || []
    //   windows.webtor.push({
    //     id: 'player',
    //     width: '100%',
    //     height: '600px',
    //     magnet: `magnet:?xt=urn:btih:${
    //       typeof quality === 'string'
    //         ? quality
    //         : (this.listDetail as any).torrents[0].hash
    //     }`,

    //     title: (this.listDetail as any).title_long,
    //     on: function (e: any) {
    //       if (e.name == windows.webtor.INITED) {
    //         // player.style.display = 'block'
    //         // select.style.display = 'block'
    //         loadVideo.style.display = 'none'

    //         player.scrollIntoView({
    //           behavior: 'smooth',
    //           block: 'start',
    //           inline: 'nearest',
    //         })
    //         vm.isLoadTorrentFinish = true
    //       }

    //       if (e.name == windows.webtor.TORRENT_ERROR) {
    //         alert('Torrent error!')
    //       }
    //     },
    //   })
    // },

    handleDisplayQuality(quality: any) {
      let coverQuality = ''
      if (quality) {
        for (const value of quality) {
          coverQuality +=
            value.quality + value.type.toString().toUpperCase() + ' '
        }
      }
      return coverQuality
    },
  },

  computed: {
    totalPage(): number {
      return Math.ceil(this.movie_count / this.limit)
    },
  },

  watch: {
    page() {
      this.handleSearch()
    },
    isLoadTorrentFinish() {
      if (this.isLoadTorrentFinish && this.isClickSkip) {
        const loadVideo = document.getElementById('loadVideo') as any
        const ads = document.getElementById('ads') as any
        loadVideo.style.display = 'none'
        ads.style.display = 'none'
        this.handleShownVideo()
      }
    },
  },
})
</script>
<style scoped lang="scss">
.view-detail {
  visibility: hidden;
  opacity: 0;
  transition: opacity 0.7s, visibility 0.7s;
}
.cart:hover .view-detail {
  visibility: visible;
  opacity: 1;
  transition: opacity 0.7s, visibility 0.7s;
}
.detail:hover .image {
  opacity: 0.2;
}
::v-deep ._jEfX5Q0_jUfq3jzoDCj {
  height: 500px;
}
:deep(._jEfX5Q0_jUfq3jzoDCj) {
  height: 500px;
}
::v-deep {
  #player {
    .frvBxo3OzNO6g_x_mz5H {
      display: none !important;
    }
  }
  .mboJcBcmq4BzeSkocC95 {
    display: none !important;
    height: 10px !important;
  }
  iframe {
    iframe {
      display: none !important;
    }
  }
  .v-pagination {
    color: whitesmoke !important;
  }
  .v-pagination__item {
    border: 1px solid #333 !important;
    color: whitesmoke !important;
    background: #171717 !important;
    font-weight: bold;
    font-size: 16px;
  }
  .v-pagination__navigation {
    border: 1px solid #333 !important;
    color: whitesmoke !important;
    background: #171717 !important;
    font-weight: bold;
    font-size: 16px;
  }
  .v-pagination__item--active {
    background: #6ac045 !important;
  }
  .v-pagination i {
    color: whitesmoke !important;
  }
  .v-application .primary {
    background-color: #6ac045 !important;
    border-color: #6ac045 !important;
  }
  .v-list-item__title {
    text-transform: capitalize;
  }
  .v-card {
    border: none;
    border-radius: 0;
    background: #1d1d1d;
    color: whitesmoke;
  }
}
#loadVideo {
  display: none;
}
#spinner {
  position: absolute;
  top: 70px;
  left: 10px;
}
#select {
  display: none;
}
</style>
