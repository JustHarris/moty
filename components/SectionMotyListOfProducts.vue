<template>
  <!-- Error/empty state -->
  <SectionUndefined
    v-if="!features.length"
    heading="Multiple products"
    description="No features added"
  ></SectionUndefined>

  <section v-else :class="`bg-${bgColor}`" class="text-center px-6 py-16 lg:px-8 xl:px-20">
    <MotyHeading
      :heading-text="heading"
      base-size="medium"
      heading-position="center"
      :class="bgColor === 'moty-lightest' ? 'text-moty-darkest' : 'text-moty-lightest'"
    ></MotyHeading>
    <div class="container mx-auto">
      <div class="grid grid-cols-4 gap-4">
        <div
          v-for="(feature, index) in features"
          :key="id + 'multiFeature' + index"
          class="mx-3 my-6 lg:mx-5 flex-1"
        >
          <VisualMedia
            v-if="feature.image && (feature.image.file || feature.image.url)"
            :source="feature.image"
            :is-background="false"
            :style-inline-img="''"
            :img-extra-class="'object-contain object-right'"
            sizes="(min-width: 276px, max-width: 276px) 50vw, 100vw"
          />

          <h3 v-if="feature">{{ feature.title }}</h3>
          <span v-if="feature">{{ feature.price }}</span>
        </div>
      </div>
      <MotyButton :links="links"></MotyButton>
    </div>
  </section>
</template>

<script>
export default {
  name: 'SectionMotyListOfProducts',
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
    links: {
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
