<template>
  <!-- Error/empty state -->
  <SectionUndefined
    v-if="!title && !image"
    heading="Full width media Image"
    description="No heading or media added"
  ></SectionUndefined>

  <!-- Skeleton loader -->
  <div
    v-else-if="fetchIsPending"
    class="py-20 bg-primary-lighter flex flex-col justify-center items-center"
  >
    <div class="loader-el w-1/2 h-7 mb-2"></div>
    <div class="loader-el w-1/3 h-7 mb-6"></div>
    <div class="loader-el w-3/5 h-2 mb-4"></div>
    <div class="loader-el w-2/5 h-2 mb-8"></div>
    <div class="loader-el w-40 h-10"></div>
  </div>

  <!-- Section content -->
  <div v-else :class="`bg-${bgColor}`" class="overflow-auto">
    <section class="relative overflow-hidden">
      <!-- Background image -->
      <VisualMedia
        v-if="image && (image.file || image.url)"
        :source="image"
        :is-background="true"
        :style-inline-img="''"
        :img-extra-class="'object-contain object-right'"
        sizes="(min-width: 768px) 50vw, 100vw"
      />
      <div class="bg-right bg-contain" :style="{ backgroundImage: 'url(' + image + ')' }"></div>
      <div
        :class="[
          { 'p-6 sm:p-7 lg:p-8 xl:p-20': outerSpacingX === 'none' && innerSpacing === 'md' },
          { 'p-6 sm:p-7 lg:p-8 xl:p-20': outerSpacingX === 'none' && innerSpacing === 'sm' },
          { 'p-8 sm:p-12 md:p-16 lg:p-20': outerSpacingX === 'md' && innerSpacing === 'md' },
          { 'p-8 md:p-12 lg:p-16': outerSpacingX === 'md' && innerSpacing === 'sm' }
        ]"
        class="relative"
      >
        <!-- Text content -->
        <div
          :class="{
            'max-w-80 md:max-w-96': alignX === 'left',
            'mx-auto text-center max-w-112': alignX === 'center',
            'ml-auto max-w-80 md:max-w-96': alignX === 'right',
            'mt-4 mb-24 md:mt-0': innerSpacing === 'md' && alignY === 'top',
            'my-12': innerSpacing === 'md' && alignY === 'center',
            'mb-4 mt-24 md:mb-0': innerSpacing === 'md' && alignY === 'bottom'
          }"
        >
          <ul class="list-horizontal">
            <li
              v-for="(feature, index) in features"
              :key="'label-product' + index"
              class="float-left text-sm"
              :class="{ 'mx-5': index > 0 }"
            >
              {{ feature.label }}
            </li>
          </ul>
          <div
            v-balance-text
            :class="{ 'text-primary-lightest': textColor === 'light' }"
            class="mb-3 text-3xl sm:text-4xl md:text-5xl lg:text-6xl"
            v-html="title"
          ></div>
          <!-- Tell prettier not to add extra whitespace -->
          <!-- display: inline -->
          <p
            v-balance-text.children
            :class="{ 'text-primary-lighter': textColor === 'light' }"
            class="whitespace-pre-line"
            v-html="description"
          >
          </p>
          <div :class="{ '-ml-3': alignX !== 'center' }">
            <BaseLink
              v-for="(link, index) in links"
              :key="id + 'link' + index"
              :link="link"
              :class="{
                'cta-link mt-5 mb-1 mx-3': link.style === 'text',
                'btn mt-6 mx-3': link.style === 'button_primary',
                light: textColor === 'light'
              }"
            ></BaseLink>
          </div>
        </div>
        <!-- END Text content -->
      </div>
    </section>
  </div>
</template>

<style>
.list-horizontal {
  list-style-type: none;
  margin: 0;
  padding: 0;
  overflow: hidden;
}
</style>

<script>
export default {
  name: 'SectionMotyFullWidthMediaImage',

  props: {
    fetchIsPending: {
      type: Boolean,
      default: true
    },
    id: {
      type: String,
      default: ''
    },
    type: {
      type: String,
      default: ''
    },
    features: {
      type: Array,
      default: () => []
    },
    title: {
      type: String,
      default: ''
    },
    description: {
      type: String,
      default: ''
    },
    image: {
      type: [Object, String],
      default: () => ({})
    },
    links: {
      type: Array,
      default: () => []
    },
    textColor: {
      type: String,
      default: 'light'
    },
    darkenBg: {
      type: Number,
      default: 0
    },
    innerSpacing: {
      type: String,
      default: 'md'
    },
    outerSpacingX: {
      type: String,
      default: 'md'
    },
    outerSpacingY: {
      type: String,
      default: 'lg'
    },
    alignX: {
      type: String,
      default: 'left'
    },
    alignY: {
      type: String,
      default: 'top'
    },
    bgColor: {
      type: String,
      default: 'primary-lightest'
    }
  }
}
</script>
