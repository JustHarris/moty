<template>
  <div class="w-auto">
    <BaseLink
      v-for="(link, index) in links"
      :key="'link' + index"
      :link="link"
      :class="{
        'cta-link mt-5 mb-1 mx-3': link.style === 'text',
        'btn mt-6 w-full bg-moty-okmed': link.style === 'button_primary',
        'btn mt-6 w-full bg-moty-transparent border-solid border border-moty-dark':
          link.style === 'button_outline',
        'btn bg-moty-okmed': link.style === 'button_primary_adjusted'
      }"
      class="text-moty-lightest"
    ></BaseLink>
  </div>
</template>

<script>
export default {
  name: 'MotyButton',
  props: {
    links: {
      type: Array,
      default: () => [
        {
          style: {
            type: String,
            default: 'button_outline'
          }
        }
      ]
    }
  }
}
</script>
