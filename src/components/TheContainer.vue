<template>
  <main>
    <div v-if="step === 1" class="feed">
      <card-post v-for="post in posts"
        :post="post"
        :key="posts.indexOf(post)">
      </card-post>
    </div>
    <div v-if="step === 2">
      <div class="selected-image"
          :class="selectedFilter"
          :style="{ backgroundImage: 'url(' + image + ')' }"></div>
      <div class="filter-container">
        <card-filter v-for="filter in filters"
          :filter="filter"
          :image="image"
          :key="filters.indexOf(filter)"
          @filter-selected="handleFilterSelected">
        </card-filter>
      </div>
    </div>
    <div v-if="step === 3">
      <div class="selected-image"
        :class="selectedFilter"
        :style="{ backgroundImage: 'url(' + image + ')' }"></div>
      <div class="caption-container">
        <textarea class="caption-input"
          placeholder="Write a caption..."
          type="text"
          :value="value"
          @input="$emit('input', $event.target.value)">
        </textarea>
      </div>
    </div>
  </main>
</template>

<script>
import CardPost from './CardPost'
import CardFilter from './CardFilter'

export default {
  name: 'TheContainer',
  data () {
    return {
      selectedFilter: ''
    }
  },
  props: {
    step: Number,
    posts: Array,
    filters: Array,
    image: String,
    value: String
  },
  components: {
    CardPost,
    CardFilter
  },
  methods: {
    handleFilterSelected (ev) {
      this.selectedFilter = ev.filter
      this.$emit('filter-selected', { filter: ev.filter })
    }
  }
}
</script>

<style lang="scss">
main {
  overflow: auto;
  height: calc(100vh);
  width: 100vw;
}

.caption-container {
  height: 210px;
  display: flex;
  align-items: center;
  justify-content: center;

  textarea {
    border: 0;
    font-size: 1rem;
    padding: 10px;
    border-bottom: 1px solid #eeeeee;
  }

  textarea:focus {
    outline: 0;
  }
}

.selected-image {
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center center;
  height: 330px;
}

.filter-container {
  display: grid;
  grid-template-columns: auto auto auto auto;
  padding: 30px 10px;
}

.feed {
  height: 100%;
  overflow-y: scroll;
  overflow-x: hidden;
  padding: 50px 0;
}
</style>
