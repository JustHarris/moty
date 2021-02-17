<template>
  <!-- Error/empty state -->
  <SectionUndefined
    v-if="!heading || !text || !image"
    heading="Text With Image"
    description="Missing heading, text or image"
  ></SectionUndefined>

  <!-- Section content -->
  <section v-else class="relative container overflow-hidden mb-10">
    <div class="relative container flex items-stretch justify-between items-stretch">
      <div v-if="imgPosition == 'left'" class="p-10 w-1/2">
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
      </div>
      <div class="p-10 w-1/2">
        <MotyHeading :heading="heading" base-size="small" heading-position="left"></MotyHeading>
        <p class="moty-text-medium text-moty-dark" v-html="text"></p>
      </div>
      <div v-if="imgPosition == 'right'" class="p-10 w-1/2">
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
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'SectionMotyTextWithImage',
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
    text: {
      type: String,
      default: 'title'
    },
    image: {
      type: [Object, String],
      default: () => ({})
    },
    imgPosition: {
      type: String,
      default: 'left'
    },
    imgBgcolor: {
      type: String,
      default: 'center'
    }
  }
}
</script>
