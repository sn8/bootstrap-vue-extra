<template>
  <b-pagination-nav
    v-if="hasPages"
    v-model="current"
    :link-gen="linkGen"
    :number-of-pages="numberOfPages"
    class="mt-4"
    @input="onInput"
  />
</template>

<script>
export default {
  name: 'Pagination',

  props: {
    total: {
      type: Number,
      required: true
    },

    limit: {
      type: Number,
      required: true
    },

    page: {
      type: Number,
      default: 1
    }
  },

  data () {
    return {
      current: this.page
    }
  },

  computed: {
    numberOfPages () {
      return Math.ceil(this.total / this.limit)
    },

    hasPages () {
      return this.numberOfPages > 0
    }
  },

  methods: {
    linkGen () {
      return ''
    },

    onInput () {
      this.$emit('goto', this.current)
    }
  }
}
</script>
