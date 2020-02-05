<template>
  <div class="toastr">
    <transition-group name="toastr">
      <div
        v-for="toast in toasts"
        :key="toast.id"
        :class="toast.class"
        class="toastr-toast alert"
      >
        {{ toast.message }}
        <button
          type="button"
          class="close"
          aria-label="Close"
          @click="close(toast.id)"
        >
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
    </transition-group>
  </div>
</template>

<script>
export default {
  name: 'Toastr',

  props: {
    bus: {
      required: true
    },

    timeout: {
      type: Number,
      default: 5000
    }
  },

  data: () => ({
    toasts: []
  }),

  mounted () {
    this.bus.$on('toast', this.createToast)
  },

  beforeDestroy () {
    this.bus.$off('toast', this.createToast)
  },

  methods: {
    /**
     * createToast
     * @param {object} toast
     */
    createToast ({ type, message }) {
      const id = Date.now()

      this.toasts.unshift({
        id,
        class: (type ? `alert-${type}` : 'alert-info'),
        message
      })

      setTimeout(() => this.close(id), this.timeout)
    },

    /**
     * close
     * @param {number} id
     */
    close (id) {
      const index = this.toasts.findIndex(toast => toast.id === id)

      if (index !== -1) {
        this.toasts.splice(index, 1)
      }
    }
  }
}
</script>

<style>
  .toastr {
    position: fixed;
    width: 20rem;
    top: 2rem;
    right: 1rem;
    cursor: default;
    z-index: 9999;
  }

  .toastr-toast {
    width: 20rem;
    transition: all .5s;
    border: unset;
    border-radius: unset;
    box-shadow: 0 1px 6px rgba(0, 0, 0, .13);
  }

  .toastr-enter {
    opacity: 0;
    transform: translateY(-3rem);
  }

  .toastr-leave-to {
    opacity: 0;
    transform: translateX(18rem);
  }

  .toastr-leave-active {
    position: absolute;
  }
</style>
