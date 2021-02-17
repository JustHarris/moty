<template>
  <!-- Error/empty state -->
  <SectionUndefined
    v-if="!reviews.length"
    heading="Customer reviews"
    description="No reviews added"
  />

  <section v-else class="relative container my-14 lg:my-16">
    <!-- Reviews -->
    <div class="flex justify-center flex-col ">
      <MotyHeading
        :heading-text="heading"
        base-size="medium"
        heading-position="center"
      ></MotyHeading>
      <div
        v-if="currentReview"
        ref="quote"
        class="relative w-full transition-all ease-in-out duration-300"
      >
        <!-- Review content -->
        <transition
          enter-active-class="transition-all duration-200 ease-out"
          :enter-class="
            animationDirection === 'left' ? 'opacity-0 translate-x-5' : 'opacity-0 -translate-x-5'
          "
          enter-to-class="opacity-100"
          leave-active-class="transition-all duration-200 ease-in"
          leave-class="opacity-100"
          :leave-to-class="
            animationDirection === 'left' ? 'opacity-0 -translate-x-5' : 'opacity-0 translate-x-5'
          "
          mode="out-in"
          @before-enter="setMaxElHeight"
        >
          <div ref="quoteContent" :key="currentReview.id">
            <div
              class="relative flex items-center justify-center text-left px-16 md:px-28 lg:px-48"
            >
              <div class="mb-4 max-w-1/2 min-w-1/3">
                <h3 class="mb-4">
                  {{ currentReview.name }}
                </h3>
                <p v-if="currentReview.location" class="mb-4">
                  {{ currentReview.location }}
                </p>
                <p v-balance-text class="mb-4">
                  {{ currentReview.quote || 'No quote added' }}
                </p>
              </div>
              <div class="mb-4 max-w-1/2 min-w-1/3 pl-10" style="height:440px">
                <VisualMedia
                  v-if="currentReview.image"
                  :source="currentReview.image"
                  :quality="100"
                  :alt="currentReview.name"
                  :widths="[310]"
                  sizes="310px"
                  class="rounded"
                  style-inline-img="width: 310px; height: 440px"
                />
              </div>
            </div>
          </div>
        </transition>
        <!-- Arrows -->
        <div v-if="reviews.length > 1" class="relative flex items-center justify-center">
          <button
            title="Previous review"
            class="p-2 rounded-full bg-moty-lightest"
            @click.prevent="prevReview"
          >
            <BaseIcon icon="uil:angle-left" size="w-8 h-8" class="text-moty-okmed" />
          </button>

          <button
            title="Next review"
            class="p-2 rounded-full bg-moty-lightest"
            @click.prevent="nextReview"
          >
            <BaseIcon icon="uil:angle-right" size="w-8 h-8" class="text-moty-okmed" />
          </button>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'SectionCustomerReviews',

  props: {
    type: {
      type: String,
      default: null
    },
    id: {
      type: String,
      default: null
    },
    heading: {
      type: String,
      default: 'What our customers say'
    },
    reviews: {
      type: Array,
      default: () => []
    }
  },

  data() {
    return {
      currentReviewIndex: 0,
      animationDirection: null
    }
  },

  computed: {
    currentReview() {
      return this.reviews[this.currentReviewIndex]
    }
  },

  mounted() {
    this.setMaxElHeight()
  },

  methods: {
    nextReview() {
      const { reviews } = this
      if (reviews) {
        this.animationDirection = 'left'
        this.currentReviewIndex < reviews.length - 1
          ? this.currentReviewIndex++
          : (this.currentReviewIndex = 0)
      }
    },
    prevReview() {
      const { reviews } = this
      if (reviews) {
        this.animationDirection = 'right'
        this.currentReviewIndex > 0
          ? this.currentReviewIndex--
          : (this.currentReviewIndex = reviews.length - 1)
      }
    },
    setMaxElHeight(el) {
      this.$nextTick(() => {
        const container = this.$refs.quote
        const content = this.$refs.quoteContent
        if (content) container.style.height = `${content.offsetHeight}px`
      })
    }
  }
}
</script>
