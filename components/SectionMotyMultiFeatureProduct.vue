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
      :class="bgColor === 'moty-lightest' ? 'text-moty-darkest' : 'text-moty-lightest'"
    ></MotyHeading>
    <div class="container mx-auto">
      <div class="flex flex-wrap justify-center mt-6">
        <MotyCard v-for="(feature, index) in features" :key="id + 'multiFeature' + index">
          <MotyTag v-if="feature" :colored="colorTag">{{ feature.tag }}</MotyTag>

          <VisualMedia
            v-if="feature.image && (feature.image.file || feature.image.url)"
            :source="feature.image"
            :is-background="false"
            :style-inline-img="''"
            :img-extra-class="'object-contain object-right'"
            sizes="(min-width: 768px) 50vw, 100vw"
          />

          <h3 v-if="feature">{{ feature.title }}</h3>
          <span v-if="feature">{{ feature.price }}</span>

          <p
            v-if="feature"
            :class="{
              'text-moty-darkest': bgColor === 'moty-lightest',
              'text-moty-lightest': bgColor === 'moty-darker'
            }"
            class="text-lg mt-4"
          >
            {{ feature.description }}
          </p>

          <MotyButton :links="feature.links"></MotyButton>
        </MotyCard>
      </div>
    </div>
  </section>
</template>

<script>
import MotyButton from './MotyButton'
import MotyTag from './MotyTag'
import MotyCard from './MotyCard'
export default {
  name: 'SectionMotyMultiFeatureProduct',
  components: {
    MotyButton,
    MotyTag,
    MotyCard
  },
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
      default: 'moty-lightest'
    }
  },
  data: function() {
    return {
      colorTag: 'bg-moty-dark'
    }
  }
}
</script>
