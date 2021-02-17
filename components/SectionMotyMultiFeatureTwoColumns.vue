<template>
  <!-- Error/empty state -->
  <SectionUndefined
    v-if="!features.length"
    heading="Multiple features"
    description="No features added"
  ></SectionUndefined>

  <section v-else :class="`bg-${bgColor}`" class="text-center px-6 py-16 lg:px-8 xl:px-20">
    <MotyHeading
      :heading-text="heading"
      base-size="medium"
      heading-position="center"
      :class="{
        'text-moty-darkest': bgColor === 'moty-lightest',
        'text-moty-lightest': bgColor === 'moty-darker'
      }"
    ></MotyHeading>
    <div class="container mx-auto">
      <div class="grid grid-cols-2 gap-4">
        <div
          v-for="(feature, index) in features"
          :key="id + 'multiFeature' + index"
          class="mx-3 my-6 lg:mx-5 flex-1"
        >
          <div
            v-if="feature"
            class="relative rounded-full bg-primary-light mx-auto w-16 h-16 float-left"
          >
            <BaseIcon :icon="feature.icon" size="lg" class="absolute center-xy"></BaseIcon>
          </div>
          <p
            v-if="feature"
            :class="{
              'text-moty-darkest': bgColor === 'moty-lightest',
              'text-moty-lightest': bgColor === 'moty-darker'
            }"
            class="text-2xl mt-4 text-left"
          >
            {{ feature.label }}
          </p>
          <p
            v-if="feature"
            :class="{
              'text-moty-darkest': bgColor === 'moty-lightest',
              'text-moty-lightest': bgColor === 'moty-darker'
            }"
            class="text-lg mt-4 text-left"
          >
            {{ feature.description }}
          </p>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'SectionMontyMultiFeatureTwoColumns',

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
      default: ''
    },
    features: {
      type: Array,
      default: () => []
    },
    bgColor: {
      type: String,
      default: 'moty-lighter'
    }
  }
}
</script>
