<template>
  <div class="image-blur" :style="styleDimensions">
    <img class="image-blur__thumb" ref="thumb" src="">
    <img class="image-blur__large" ref="image" src="" :class="{'loaded': loaded}" v-if="loadedThumb">
  </div>
</template>

<script>
export default {
  props: {
    image: {
      type: String
    },
    thumb: {
      type: String
    },
    width: {
      type: String
    },
    height: {
      type: String
    }
  },
  data () {
    return {
      loaded: false,
      loadedThumb: false
    }
  },
  methods: {
    async initLoad () {
      this.loaded = false
      this.loadedThumb = false
      try {
        await this.handleLoadThumb()
        this.loadedThumb = true
        this.$nextTick(async () => {
          await this.handleLoadImage()
        })
      } catch (e) {
        console.log(e)
      }
    },
    loadImage (image, url) {
      return new Promise((resolve, reject) => {
        const downloadingImage = new Image()
        downloadingImage.onload = function () {
          image.src = this.src
          resolve()
        }
        downloadingImage.onerror = () => {
          reject()
        }
        downloadingImage.src = url
      })
    },
    async handleLoadThumb () {
      const thumb = this.$refs.thumb
      if (!thumb) return
      await this.loadImage(thumb, this.thumb)
    },
    async handleLoadImage () {
      const image = this.$refs.image
      if (!image) return
      await this.loadImage(image, this.image)
      setTimeout(() => {
        this.loaded = true
      }, 20)
    }
  },
  computed: {
    styleDimensions () {
      const dimensions = {}
      if (this.width) dimensions.width = this.width + 'px'
      if (this.height) dimensions.height = this.height + 'px'
      return dimensions
    }
  },
  watch: {
    image () {
      this.initLoad()
    }
  },
  mounted () {
    this.initLoad()
  }
}
</script>
