<template>
  <b-form @submit.prevent="$emit('submit', form)">
    <b-form-group
      v-for="field in fields"
      :key="field.name"
      :label="field.label || getLabelName(field.name)"
      :label-for="field.name"
    >
      <component
        :is="field.component"
        v-model="form[field.name]"
        v-bind="field.attrs"
        :id="field.name"
        :required="field.required || false"
      />
    </b-form-group>
    <loading-button
      :is-loading="isLoading"
      type="submit"
    />
  </b-form>
</template>

<script>
import LoadingButton from './LoadingButton.vue'

export default {
  name: 'DeclarativeForm',

  components: {
    LoadingButton
  },

  props: {
    value: {
      type: Object,
      required: true
    },

    fields: {
      type: Array,
      required: true
    },

    isLoading: {
      type: Boolean,
      default: false
    }
  },

  watch: {
    value: {
      handler (value) {
        this.form = { ...value }
      },
      deep: true
    }
  },

  data: () => ({
    form: {}
  }),

  mounted () {
    this.form = { ...this.value }
  },

  methods: {
    getLabelName (name) {
      return name.replace(/([A-Z])/g, ' $1').replace(/^./, (str) => str.toUpperCase()) + ':'
    }
  }
}
</script>
