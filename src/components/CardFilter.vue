<template>
  <div class="card-filter">
    <p>{{filter.name}}</p>
    <div class="img"
      :class="filter.name"
      :id="filter.name"
      :style="{ backgroundImage: 'url(' + image + ')' }"
      @click="selectFilter">
    </div>
  </div>
</template>

<script>
export default {
  name: 'CardFilter',
  props: {
    filter: Object,
    image: String
  },
  methods: {
    selectFilter (ev) {
      ev.preventDefault()
      this.$emit('filter-selected', { filter: ev.target.id })
    }
  }
}
</script>

<style lang="scss">
.card-filter {
  display: inline-block;
  margin: 0 3px;
  box-sizing: border-box;
  p {
    font-size: 11px;
    text-align: center;
    text-transform: capitalize;
    padding-bottom: 5px;
  }
  .img {
    cursor: pointer;
    height: 100px;
    background-size: cover;
    background-position: center center;
  }
}
.card-filter:last-child {
  margin-right: 20px;
}
</style>
