<template>
  <div>
    <the-header
      :step="step"
      @go-to-home="handleGoToHome"
      @next-step="step++"
      @share-post="handleSharePost"/>
    <the-container
      :step="step"
      :posts="posts"
      :filters="filters"
      :image="image"
      v-model="caption"
      @filter-selected="handleFilterSelected"
    />
    <the-footer
      :step="step"
      @go-to-home="handleGoToHome"
      @upload-image="handleUploadImage"/>
  </div>
</template>

<script>
import TheHeader from '@/components/TheHeader.vue'
import TheContainer from '@/components/TheContainer.vue'
import TheFooter from '@/components/TheFooter.vue'

import posts from '@/data/posts'
import filters from '@/data/filters'

export default {
  name: 'Home',
  data () {
    return {
      posts,
      filters,
      caption: '',
      image: '',
      step: 1
    }
  },
  components: {
    TheHeader,
    TheContainer,
    TheFooter
  },
  methods: {
    handleGoToHome () {
      this.caption = ''
      this.image = ''
      this.step = 1
    },
    handleSharePost () {
      const post = {
        username: 'VueVixens',
        userImage:
          'data:image/png;base64,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',
        postImage: this.image,
        likes: 0,
        caption: this.caption,
        filter: this.filterType
      }
      this.posts.unshift(post)
      this.handleGoToHome()
    },
    handleUploadImage (ev) {
      const files = ev.target.files
      if (!files.length) return

      const reader = new FileReader()
      reader.readAsDataURL(files[0])
      reader.onload = ev => {
        this.image = ev.target.result
        this.step = 2
      }
      document.querySelector('#file').value = ''
    },
    handleFilterSelected (ev) {
      this.filterType = ev.filter
    }
  }
}
</script>
