<template>
  <div class="image-blur" :style="styleDimensions">
    <img class="image-blur__thumb"
      ref="thumb"
      :src="thumb"
      @load="onThumbLoaded">
    <img class="image-blur__large"
      ref="image"
      :src="image"
      @load="onImageLoaded"
      :class="{'loaded': loadedImage}"
      v-if="loadedThumb">
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
      loadedImage: false,
      loadedThumb: false
    }
  },
  methods: {
    async initLoad () {
      this.loadedImage = false
      this.loadedThumb = false
    },
    onThumbLoaded () {
      this.loadedThumb = true
    },
    onImageLoaded () {
      setTimeout(() => {
        this.loadedImage = true
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
