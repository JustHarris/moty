<template>
  <div :class="colored" class="rounded-full py-1 px-3 text-xs text-moty-lightest float-left">
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: 'MotyTag',
  props: {
    colored: {
      type: String,
      default: ''
    }
  }
}
</script>
