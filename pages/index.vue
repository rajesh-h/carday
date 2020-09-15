<template>
  <div class="container mx-auto">
    <Header class="flow-root" />
    <Slider :slides-data="slidesData" />
  </div>
</template>

<script>
import Header from '~/components/Header'
import Slider from '~/components/Slider'

export default {
  components: {
    Slider,
    Header,
  },
  async asyncData({ $content, params }) {
    const slidesData = await $content('slides')
      .only(['title', 'thumbnail', 'description'])
      .sortBy('createdAt', 'desc')
      .limit(12)
      .fetch()
    return {
      slidesData,
    }
  },
  head() {
    return {
      script: [
        { src: 'https://identity.netlify.com/v1/netlify-identity-widget.js' },
      ],
    }
  },
}
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
@apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
.container {
  max-width: 100%;
  margin: 0 auto;
  min-height: 100vh;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
