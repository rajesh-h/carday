<template>
  <div class="w-full">
    <client-only>
      <vue-flux
        ref="slider"
        :options="vfOptions"
        :images="slideImages"
        :transitions="vfTransitions"
        :captions="slideCaptions"
      >
        <template v-slot:preloader>
          <flux-preloader />
        </template>

        <!-- <template v-slot:caption>
          <flux-caption />
        </template> -->
        <template v-slot:caption>
          <flux-caption v-slot="captionProps">
            <div
              class="text-3xl text-white font-black bg-transparent px-6 py-4"
            >
              {{ captionProps.text }}
            </div>
            <div
              class="text-base text-white font-semibold bg-transparent pt-0 pb-2 px-6"
            >
              {{ captionProps.caption.description }}
            </div>
            <a
              :href="captionProps.caption.targeturl"
              class="text-lg text-black font-bold bg-white px-4 py-2 mx-6"
            >
              {{ captionProps.caption.buttontext }}
            </a>
          </flux-caption>
        </template>

        <template v-slot:controls>
          <flux-controls />
        </template>

        <!-- <template v-slot:pagination>
          <flux-pagination />
        </template>

        <template v-slot:index>
          <flux-index />
        </template> -->
      </vue-flux>

      <!-- <button @click="$refs.slider.show('next')">NEXT</button> -->
    </client-only>
  </div>
</template>

<script>
import {
  VueFlux,
  FluxCaption,
  FluxControls,
  // FluxIndex,
  // FluxPagination,
  FluxPreloader,
} from 'vue-flux/dist-ssr/vue-flux.umd.min.js'

import 'vue-flux/dist-ssr/vue-flux.css'

export default {
  components: {
    VueFlux,
    FluxCaption,
    FluxControls,
    // FluxIndex,
    // FluxPagination,
    FluxPreloader,
  },
  props: {
    slidesData: {
      type: Array,
      default: null,
    },
  },
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
    // vfImages: [
    //   'https://source.unsplash.com/weekly?water',
    //   'https://source.unsplash.com/weekly?mountain',
    //   'https://source.unsplash.com/daily',
    //   '/img/slide1.jpeg',
    // ],
    vfTransitions: ['fade', 'cube', 'book', 'wave'],
    // vfCaptions: [
    //   'Caption for image 1',
    //   'Caption for image 2',
    //   'Caption for image 3',
    // ],
    captionProps: {
      caption: String | Object,
      text: String,
    },
  }),
  computed: {
    slideImages() {
      const images = []
      for (let i = 0; i < this.slidesData.length; i++) {
        images.push(this.slidesData[i].thumbnail)
      }
      return images
    },
    slideCaptions() {
      const captions = []
      for (let i = 0; i < this.slidesData.length; i++) {
        captions.push({
          description: this.slidesData[i].description,
          targeturl: this.slidesData[i].targeturl,
          buttontext: this.slidesData[i].buttontext,
          text: this.slidesData[i].title,
        })
      }
      return captions
    },
  },
}
</script>

<style>
.vue-flux {
  height: 80vh !important;
  width: 100% !important;
}

.vue-flux .flux-caption {
  background-color: transparent !important;
  text-align: left !important;
  margin-top: 10% !important;
  width: 500px !important;
  line-height: 2rem !important;
}
</style>
