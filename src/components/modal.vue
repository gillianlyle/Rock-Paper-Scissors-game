<template id="modal-template">
  <div class="modal-mask">
    <div class="modal-wrapper">
      <div class="modal-container">
        <div class="modal-header">
          <slot name="header">
            default header
          </slot>

          <button
            class="btn"
            @click="$emit('close')"
          >
            <img
              src="../assets/images/icon-close.svg"
              alt="Close modal icon"
            >
          </button>
        </div>

        <div class="modal-body">
          <slot name="body">
            default body
          </slot>
        </div>

        <div class="modal-footer">
          <slot name="footer" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
    name: 'Modal'
}
</script>