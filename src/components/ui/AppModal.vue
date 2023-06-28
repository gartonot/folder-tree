<template>
  <div
    :class="['modal', { 'modal-open': isOpen }]"
    @click="modalClose()"
  >
    <div class="modal-body" @click.stop>
      <slot name="header">
        {{ header }}
      </slot>
      <div class="button-close" @click="modalClose()">
        <close-icon class="icon" />
      </div>
      <div class="content">
        <slot/>
      </div>
      <app-button label="Ок" @click="modalClose()"/>
    </div>
  </div>
</template>

<script>
  import CloseIcon from '@/components/iconsComponents/CloseIcon.vue'
  import AppButton from '@/components/ui/AppButton.vue'

  export default {
    name: 'AppModal',
    components: {
      AppButton,
      CloseIcon
    },
    props: {
      isOpen: {
        type: Boolean,
        default: false
      },
      header: {
        type: String,
        default: ''
      }
    },
    methods: {
      modalClose() {
        this.$emit('modal-close')
      }
    }
  }
</script>

<style lang="scss" scoped>
  @import "@/assets/scss/variables.scss";
  @import "@/assets/scss/mixins.scss";

  .modal {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    backdrop-filter: blur(2px);
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    background: transparent;
    opacity: 0;
    visibility: hidden;
    transition: 0.3s;

    &-body {
      position: relative;
      max-width: 80%;
      width: 80%;
      background: $white-color;
      border-radius: 8px;
      padding: 50px 60px 40px;
      transform: scale(0);
      max-height: 80%;
      height: 600px;
      overflow: hidden;
      transition: 0.3s;

      .content {
        height: 90%;
        overflow-y: auto;
      }
    }

    &-open {
      @include background-opacity($black-color, 0.6);
      opacity: 1;
      visibility: visible;

      .modal-body {
        transform: scale(1);
      }
    }
  }

  .button-close {
    position: fixed;
    top: 10px;
    right: 12px;
    cursor: pointer;
    width: 16px;
    height: 16px;

    .icon {
      color: $error-color;
    }
  }
</style>
