<template>
  <i class="bi" :class="'bi-' + icon"></i>
</template>

<script>
export default {
  props: {
    icon: {
      type: String,
      default: 'x-lg'
    }
  }
}
</script>

<style lang="scss" scoped></style>
