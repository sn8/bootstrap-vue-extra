<template>
  <b-button
    v-bind="$attrs"
    v-on="$listeners"
    :disabled="isLoading"
  >
    <span
      v-if="isLoading"
      class="spinner-border spinner-border-sm"
      role="status"
      aria-hidden="true"
    />
    <slot>
      Submit
    </slot>
  </b-button>
</template>

<script>
export default {
  name: 'LoadingButton',

  props: {
    isLoading: {
      type: Boolean,
      default: false
    }
  }
}
</script>
