<template>
  <!-- Error/empty state -->
  <SectionUndefined
    v-if="!heading && !image"
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
  <div v-else class="overflow-auto bg-moty-lightest">
    <section class="relative overflow-hidden pb-24">
      <!-- Background image -->
      <div
        class="absolute small-ball rounded-full h-72 w-72 flex items-center justify-center bg-moty-darker"
      ></div>
      <div
        class="absolute big-ball rounded-full h-full flex items-center justify-center bg-moty-oklight"
      ></div>
      <div class="featuredImg w-15 absolute right-26 top-32">
        <VisualMedia
          v-if="image && (image.file || image.url)"
          :source="image"
          :is-background="false"
          :only-get-img="true"
          :style-inline-img="''"
          :img-extra-class="''"
          sizes="(min-width: 768px) 50vw, 100vw h-full"
        />
      </div>
      <MotyIconBorder class="absolute right-0 logo"></MotyIconBorder>
      <div class="relative container pt-44 pb-48">
        <!-- Text content -->
        <div class="max-w-80 md:max-w-96">
          <MotyHeading
            :heading-text="heading"
            base-size="large"
            heading-position="left"
            level="1"
          ></MotyHeading>
          <p
            v-balance-text.children
            class="whitespace-pre-line moty-text-large text-moty-dark"
            v-html="description"
          ></p>
        </div>
        <!-- END Text content -->
      </div>
    </section>
  </div>
</template>

<style lang="postcss" scoped>
.big-ball {
  width: 720px;
  height: 720px;
  right: -150px;
  top: -150px;
}

.small-ball {
  right: -86px;
  top: 360px;
}
.logo {
  width: 338px;
  top: -100px;
}
</style>

<script>
import MotyIconBorder from '../static/assets/moty-icon-border.svg'

export default {
  name: 'SectionMotyHeroHeader',
  components: {
    MotyIconBorder
  },
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
      default: ''
    },
    description: {
      type: String,
      default: ''
    },
    image: {
      type: [Object, String],
      default: () => ({})
    }
  }
}
</script>
