<template>
  <div
    :class="[`bg-${bgCardColor}`]"
    class="border-solid border-1 border-light-blue-500 rounded-lg shadow-xl p-7 mx-3 my-3 lg:mx-3 flex-1"
  >
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: 'MotyCard',
  props: {
    bgCardColor: {
      type: String,
      default: 'moty-lightest'
    }
  }
}
</script>
