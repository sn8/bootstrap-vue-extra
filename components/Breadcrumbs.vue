<template>
  <b-breadcrumb :items="items"/>
</template>

<script>
export default {
  name: 'Breadcrumbs',

  data: () => ({
    items: []
  }),

  watch: {
    $route () {
      this.fillBreadcrumbs()
    }
  },

  mounted () {
    this.fillBreadcrumbs()
  },

  methods: {
    fillBreadcrumbs () {
      const { matched, path: currentPath } = this.$route

      this.items = matched
        .map(v => ({
          text: v.meta.name || v.name,
          to: v.path,
          active: (
            currentPath === v.path ||
            `${currentPath}/` === v.path ||
            currentPath === `${v.path}/`
          )
        }))
    }
  }
}
</script>
