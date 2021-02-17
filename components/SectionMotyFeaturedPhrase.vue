<template>
  <!-- Error/empty state -->
  <SectionUndefined
    v-if="!text"
    heading="Featured Phrase"
    description="Missing text"
  ></SectionUndefined>

  <!-- Section content -->
  <section v-else class="relative container overflow-hidden mb-10">
    <div class="relative container h-96">
      <div class="absolute w-40 h-34" :style="bgcolor"></div>
      <div class="absolute p-10">
        <p class="absolute moty-text-medium text-moty-dark" v-html="text"></p>
      </div>
      <div class="absolute w-40 h-34" :style="bgcolor"></div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'SectionMotyFeaturedPhrase',
  props: {
    fetchIsPending: {
      type: Boolean,
      default: true
    },
    id: {
      type: String,
      default: ''
    },
    text: {
      type: String,
      default: ''
    },
    bgcolor: {
      type: String,
      default: ''
    }
  }
}
</script>
