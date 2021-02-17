<template>
  <!-- Error/empty state -->
  <SectionUndefined
    v-if="!heading || !list.length || !image"
    heading="Misc Content"
    description="Missing heading, list or image"
  ></SectionUndefined>

  <!-- Section content -->
  <section v-else class="relative container overflow-hidden mb-10">
    <MotyHeading :heading="heading" base-size="medium" heading-position="center"></MotyHeading>
    <p v-if="text" class="mb-3 moty-text-medium text-moty-dark" v-html="text"></p>
    <div class="relative container flex items-stretch justify-between items-stretch">
      <div v-if="imgPosition === 'left'" class="p-10 w-1/2">
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
        <ul>
          <li v-for="item in list" :key="item.title" class="mt-1 text-sm">
            <label class="moty-text-medium-bold text-moty-dark">{{ item.bulletTitle }}</label>
            <p class="moty-text-medium text-moty-dark" v-html="item.bulletText"></p>
          </li>
        </ul>
      </div>
      <div v-if="imgPosition === 'right'" class="p-10 w-1/2">
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
import MotyHeading from './MotyHeading'

export default {
  name: 'SectionMotyMiscContent',
  components: {
    MotyHeading,
  },
  props: {
    fetchIsPending: {
      type: Boolean,
      default: true,
    },
    id: {
      type: String,
      default: '',
    },
    heading: {
      type: String,
      default: '',
    },
    text: {
      type: String,
      default: '',
    },
    image: {
      type: [Object, String],
      default: () => ({}),
    },
    list: {
      type: Array,
      required: true,
    },
    imgPosition: {
      type: String,
      default: 'left',
    },
  },
}
</script>
