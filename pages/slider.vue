<template>
  <div>
    <client-only>
      <vue-flux
        ref="slider"
        :options="vfOptions"
        :images="vfImages"
        :transitions="vfTransitions"
        :captions="vfCaptions"
      >
        <template v-slot:preloader>
          <flux-preloader />
        </template>

        <template v-slot:caption>
          <flux-caption />
        </template>

        <template v-slot:controls>
          <flux-controls />
        </template>

        <template v-slot:pagination>
          <flux-pagination />
        </template>

        <template v-slot:index>
          <flux-index />
        </template>
      </vue-flux>

      <button @click="$refs.slider.show('next')">NEXT</button>
    </client-only>
  </div>
</template>

<script>
import {
  VueFlux,
  FluxCaption,
  FluxControls,
  FluxIndex,
  FluxPagination,
  FluxPreloader,
} from 'vue-flux/dist-ssr/vue-flux.umd.min.js'

import 'vue-flux/dist-ssr/vue-flux.css'

export default {
  components: {
    VueFlux,
    FluxCaption,
    FluxControls,
    FluxIndex,
    FluxPagination,
    FluxPreloader,
  },
  // async fetch() {
  //   const posts = await this.$content('slides').fetch()
  //   this.slides = posts
  // },
  data: () => ({
    vfOptions: {
      allowFullscreen: false,
      allowToSkipTransition: true,
      autohideTime: 2500,
      autoplay: true,
      bindKeys: false,
      delay: 5000,
      enableGestures: false,
      infinite: true,
      lazyLoad: true,
      lazyLoadAfter: 3,
    },
    vfImages: [
      'https://source.unsplash.com/weekly?water',
      'https://source.unsplash.com/weekly?mountain',
      'https://source.unsplash.com/daily',
      '/img/slide1.jpeg',
    ],
    vfTransitions: ['fade', 'cube', 'book', 'wave'],
    vfCaptions: [
      'Caption for image 1',
      'Caption for image 2',
      'Caption for image 3',
    ],
  }),
}
</script>

<style></style>
