<template>
  <div
    v-observe-visibility="{ callback: isViewableNow, once: true }"
    :class="{
      visible: showAnimation,
      [transitionName]: showAnimation,
      invisible: !showAnimation
    }"
  >
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: 'MotyTransition',
  props: {
    transitionName: {
      type: String,
      default: 'slide-top'
    }
  },
  data: function() {
    return {
      showAnimation: false
    }
  },
  methods: {
    isViewableNow(isVisible, entry) {
      this.showAnimation = isVisible
    }
  }
}
</script>
