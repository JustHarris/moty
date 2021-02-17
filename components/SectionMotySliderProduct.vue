<template>
  <!-- Error/empty state -->
  <SectionUndefined
    v-if="!features.length"
    heading="Multiple features"
    description="No features added"
  ></SectionUndefined>

  <section v-else class="text-center px-6 py-16 lg:px-8 xl:px-20 bg-moty-lightest">
    <div class="container mx-auto">
      <div class="grid grid-cols-3 gap-4">
        <MotySliderImage
          v-if="images.length > 0"
          :images="images"
          class="col-span-2"
        ></MotySliderImage>

        <MotyCard class="col-span-1 " :bg-card-color="'moty-darker'">
          <div class="text-moty-lightest text-sm grid grid-cols-2 gap-2 mb-5">
            <h4
              v-if="name"
              class="col-span-1 text-moty-okmed font-normal leading-7 text-left text-2xl"
            >
              {{ name }}
            </h4>
            <div v-if="price" class="col-span-1">
              <span class="text-right font-bold text-3xl w-full block">{{ price }}</span>
              <small class="text-sm w-full text-right w-full block">al mes</small>
            </div>
          </div>

          <div
            v-for="(feature, index) in features"
            :key="id + 'multiFeature' + index"
            class="divide-y divide-moty-dark divide-solid"
          >
            <div v-if="feature.speed" class="text-moty-lightest text-sm grid grid-cols-2 gap-2">
              <span class="col-span-1 text-left py-3">Velocidad máxima</span>
              <span class="col-span-1 text-right py-3">{{ feature.speed }}</span>
            </div>

            <div v-if="feature.autonomy" class="text-moty-lightest text-sm grid grid-cols-2 gap-2">
              <span class="col-span-1 text-left py-3">Autonomía</span>
              <span class="col-span-1 text-right py-3">{{ feature.autonomy }}</span>
            </div>

            <div
              v-if="feature.batteryTime"
              class="text-moty-lightest text-sm grid grid-cols-2 gap-2"
            >
              <span class="col-span-1 text-left py-3">Tiempo carga</span>
              <span class="col-span-1 text-right py-3">{{ feature.batteryTime }}</span>
            </div>

            <div v-if="feature.isFolding" class="text-moty-lightest text-sm grid grid-cols-2 gap-2">
              <span class="col-span-1 text-left py-3">Plegable</span>
              <span class="col-span-1 text-right py-3">{{ feature.isFolding ? 'Si' : 'No' }}</span>
            </div>

            <div v-if="feature.weight" class="text-moty-lightest text-sm grid grid-cols-2 gap-2">
              <span class="col-span-1 text-left py-3">Peso</span>
              <span class="col-span-1 text-right py-3">{{ feature.weight }}</span>
            </div>
          </div>

          <MotyButton
            v-for="(feature, index) in features"
            :key="id + 'multiFeatureLinks' + index"
            :links="feature.links"
          ></MotyButton>
        </MotyCard>
      </div>
    </div>
  </section>
</template>

<script>
import MotyButton from './MotyButton'
import MotyCard from './MotyCard'
import MotySliderImage from './MotySliderImage'
export default {
  name: 'SectionMotySliderProduct',
  components: {
    MotyButton,
    MotyCard,
    MotySliderImage
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
    name: {
      type: String,
      default: ''
    },
    price: {
      type: String,
      default: ''
    },
    images: {
      type: Array,
      default: () => []
    },
    features: {
      type: Array,
      default: () => []
    },
    direction: {
      type: String,
      default: 'left'
    }
  }
}
</script>
