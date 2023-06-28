<template>
  <button class="button" @click="$emit('click')">
    <slot>
      {{ label }}
    </slot>
  </button>
</template>

<script>
  export default {
    name: 'AppButton',
    props: {
      label: {
        type: String,
        required: true
      }
    }
  }
</script>

<style lang="scss" scoped>
  @import "@/assets/scss/variables.scss";

  .button {
    padding: 12px 24px;
    border: 1px solid $primary-color;
    color: $primary-color;
    font-weight: 600;
    border-radius: 4px;
    cursor: pointer;
    transition: 0.3s;

    &:hover {
      background: $primary-color;
      color: $white-color;
    }
  }
</style>