<template>
  <div class="relative">
    <transition-group name="fade" tag="div" class="container-slider relative">
      <div v-for="i in [currentIndex]" :key="i" class="slide" :class="slideDirection">
        <VisualMedia
          v-if="currentImg.image && (currentImg.image.file || currentImg.image.url)"
          :source="currentImg.image"
          :lazy-load="false"
          :is-background="true"
          :style-inline-img="'object-fit: contain;'"
          sizes="(min-width: 768px) 50vw, 100vw h-full"
        />
      </div>
    </transition-group>
    <a class="prev" @click="prev"><ForwardIcon /></a>
    <a class="next" @click="next"><ForwardIcon /></a>
  </div>
</template>
<script>
import ForwardIcon from '../static/assets/forward-icon.svg'
export default {
  name: 'MotySliderImage',
  components: {
    ForwardIcon
  },
  props: {
    images: {
      type: Array,
      default: () => []
    }
  },
  data() {
    return {
      timer: null,
      currentIndex: 0,
      slideDirection: 'left'
    }
  },
  computed: {
    currentImg: function() {
      return this.images[Math.abs(this.currentIndex) % this.images.length]
    }
  },
  methods: {
    next: function() {
      this.currentIndex += 1
      this.slideDirection = 'right'
    },
    prev: function() {
      this.currentIndex -= 1
      this.slideDirection = 'left'
    }
  }
}
</script>

<style lang="postcss" scoped>
.slide {
  transition: all 0.5s ease;
  position: absolute;
  width: 100%;
  height: 100%;
}

/*IN*/
.slide.left.fade-enter,
.slide.left.fade-enter-active {
  animation: bounce-in .5s;
}
.slide.right.fade-enter,
.slide.right.fade-enter-active {
  animation: bounce-in .5s;
}

/*OUT*/
.slide.right.fade-leave-to,
.slide.right.fade-leave-active {
  animation: bounce-in .5s reverse;
}

.slide.left.fade-leave-to,
.slide.left.fade-leave-active {
  animation: bounce-in .5s reverse;
}

@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.5);
  }
  100% {
    transform: scale(1);
  }
}

.container-slider {
  height: 100%;
  width: 100%;
  overflow: hidden;
}

.prev,
.next {
  cursor: pointer;
  background: var(--colors-moty-darkest);
  border-radius: 40px;
  width: 54px;
  height: 54px;
  display: inline-block;
  position: absolute;
  top: 50%;
}

.prev svg,
.next svg {
  width: 8px;
  height: 54px;
  display: inline-block;
}
.prev svg {
  margin-left: -3px;
}

.next {
  transform: rotate(-180deg);
  right: 0;
}

.prev {
  left: 0;
}

.prev:hover,
.next:hover {
  opacity: 0.8;
}
</style>
