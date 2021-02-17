<template>
  <!-- Error/empty state -->
  <SectionUndefined
    v-if="!items || items.length < 2 || items.length > 4"
    heading="Squared Explanation"
    description="Number of items not between 2-4"
  ></SectionUndefined>

  <!-- Section content -->
  <section v-else class="relative container overflow-hidden mb-10">
    <MotyHeading
      :heading-text="heading"
      base-size="medium"
      :heading-position="headingPosition"
      class="px-12"
    ></MotyHeading>
    <div class="relative container flex items-stretch justify-between items-stretch">
      <div
        v-for="item in items"
        :key="item.title"
        class="p-10"
        :class="{
          'w-1/2': items.length === 2,
          'w-1/3': items.length === 3,
          'w-1/4': items.length === 4,
          'bg-moty-okmed': item.bgColor === 'moty-okmed',
          'bg-moty-dark': item.bgColor === 'moty-dark',
          'bg-moty-darker': item.bgColor === 'moty-darker'
        }"
      >
        <div class="pb-5 w-full moty-display-small-bold text-moty-lightest">
          {{ item.title }}
        </div>
        <p class="px-5 moty-text-small text-moty-lighter" v-html="item.value"></p>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'SectionMotySquaredExplanation',
  props: {
    fetchIsPending: {
      type: Boolean,
      default: true
    },
    id: {
      type: String,
      default: ''
    },
    heading: {
      type: String,
      default: 'title'
    },
    items: {
      type: Array,
      default: () => []
    },
    headingPosition: {
      type: String,
      default: 'center'
    }
  }
}
</script>
