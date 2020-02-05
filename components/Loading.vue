<template>
  <div>
    <div
      v-if="isLoading"
      class="mt-3 loading spinner-border spinner-border-sm text-secondary"
      role="status"
    >
      <span class="sr-only">Loading...</span>
    </div>
    <slot v-else />
  </div>
</template>

<script>
export default {
  name: 'Loading',

  props: {
    isLoading: {
      type: Boolean,
      default: false
    }
  }
}
</script>
