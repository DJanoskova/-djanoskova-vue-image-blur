# @djanoskova/vue-image-blur

### Demo
See the working example at <a href="https://vue-image-blur.herokuapp.com/" target="_blank">https://vue-image-blur.herokuapp.com/</a> and the demo code repository at <a href="https://github.com/DJanoskova/-djanoskova-vue-image-blur-demo" target="_blank">https://github.com/DJanoskova/-djanoskova-vue-image-blur-demo</a>

### Component usage
```
<template>
 <ImageBlur
    width="390"
    height="500"
    :image="myImage.large"
    :thumb="myImage.thumb"/>
</template>
```
Either specify the width and height as props or style the .image-blur class to have fixed dimensions.

```
<script>
import { ImageBlur } from '@djanoskova/vue-image-blur'
import '@djanoskova/vue-image-blur/public/css/imageBlur.css'

export default {
  data () {
    return {
      myImage: {
        large: 'http://mysite.com/image_large.jpg',
        thumb: 'http://mysite.com/image_thumb.jpg'
      }
    }
  },
  components: {
    ImageBlur
  }
}
</script>
```

Check the component source for more information.