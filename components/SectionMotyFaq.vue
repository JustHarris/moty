<template>
  <!-- Error/empty state -->
  <SectionUndefined v-if="!items.length" heading="FAQ" description="No FAQ added" />

  <!-- Section content -->
  <section v-else class="relative container overflow-hidden mb-10">
    <MotyHeading :heading-text="heading" base-size="medium" heading-position="center"></MotyHeading>
    <VsaList v-bind="listOptions">
      <VsaItem v-for="item in items" :key="item.title">
        <VsaHeading
          ><div class="moty-text-large-bold">{{ item.title }}</div></VsaHeading
        >
        <VsaContent><div class="moty-text-medium" v-html="item.value"></div></VsaContent>
      </VsaItem>
    </VsaList>
  </section>
</template>
<script>
import { VsaList, VsaItem, VsaHeading, VsaContent } from 'vue-simple-accordion'

export default {
  name: 'SectionMotyFaq',

  components: {
    VsaList,
    VsaItem,
    VsaHeading,
    VsaContent
  },

  props: {
    fetchIsPending: {
      type: Boolean,
      default: true
    },
    heading: {
      type: String,
      default: 'title'
    },
    items: {
      type: Array,
      required: true
    }
  },

  data() {
    return {
      listOptions: {
        tags: {
          list: 'dl',
          list__item: 'div',
          item__heading: 'dt',
          heading__content: 'span',
          heading__icon: 'span',
          item__content: 'dd'
        },
        roles: {
          presentation: false,
          heading: false,
          region: true
        },
        transition: 'vsa-collapse',
        initActive: false,
        forceActive: undefined,
        autoCollapse: true,
        onHeadingClick: () => {},
        navigation: true
      }
    }
  }
}
</script>
<style lang="postcss" scoped>
.vsa-list {
  --vsa-min-width: 300px;
  --vsa-heading-padding: 0.75rem 0.75rem;
  --vsa-text-color: var(--colors-moty-dark);
  --vsa-heading-color: var(--colors-moty-darker);
  --vsa-highlight-color: var(--colors-transparent);
  --vsa-bg-color: var(--colors-moty-lightest);
  --vsa-border: 1px solid var(--colors-moty-darkest);
  --vsa-content-padding: 1.25rem 1.25rem;
  --vsa-default-icon-size: 0.5;
  display: block;
  min-width: var(--vsa-min-width);
  width: 100%;
  padding: 0;
  margin: 0;
  list-style: none;
  color: var(--vsa-text-color);
  background-color: var(--vsa-bg-color);
  font: var(--typography-body-font-normal);
}

.vsa-list [hidden] {
  display: none;
}

.vsa-list >>> .vsa-item__heading {
  width: 100%;
  height: 100%;
}

.vsa-list >>> .vsa-item__heading,
.vsa-list >>> .vsa-item__trigger {
  display: flex;
  justify-content: flex-start;
  align-items: center;
}

.vsa-list >>> .vsa-item__trigger {
  margin: 0;
  padding: 0;
  color: inherit;
  font-family: inherit;
  font-size: 100%;
  line-height: 1.15;
  border-width: 0;
  background-color: transparent;
  background-image: none;
  overflow: visible;
  text-transform: none;
  flex: 1 1 auto;
  color: var(--vsa-text-color);
  transition: all 0.2s linear;
  padding: var(--vsa-heading-padding);
}

.vsa-list >>> .vsa-item__trigger[role='button'] {
  cursor: pointer;
}

.vsa-list >>> .vsa-item__trigger[type='button'],
.vsa-list >>> .vsa-item__trigger[type='reset'],
.vsa-list >>> .vsa-item__trigger[type='submit'] {
  -webkit-appearance: button;
}

.vsa-list >>> .vsa-item__trigger:focus {
  outline: 1px dotted;
  outline: 5px auto -webkit-focus-ring-color;
}

.vsa-list >>> .vsa-item__trigger::-moz-focus-inner,
.vsa-list >>> .vsa-item__trigger[type='button']::-moz-focus-inner,
.vsa-list >>> .vsa-item__trigger[type='reset']::-moz-focus-inner,
.vsa-list >>> .vsa-item__trigger[type='submit']::-moz-focus-inner {
  border-style: none;
  padding: 0;
}

.vsa-list >>> .vsa-item__trigger:-moz-focusring,
.vsa-list >>> .vsa-item__trigger[type='button']:-moz-focusring,
.vsa-list >>> .vsa-item__trigger[type='reset']:-moz-focusring,
.vsa-list >>> .vsa-item__trigger[type='submit']:-moz-focusring {
  outline: 1px dotted ButtonText;
}

.vsa-list >>> .vsa-item__trigger:focus,
.vsa-list >>> .vsa-item__trigger:hover {
  outline: none;
  background-color: var(--vsa-highlight-color);
  color: var(--vsa-text-color);
}

.vsa-list >>> .vsa-item__trigger__icon--is-default {
  width: 40px;
  height: 40px;
  transform: scale(var(--vsa-default-icon-size));
}

.vsa-list >>> .vsa-item__trigger__icon--is-default:after,
.vsa-list >>> .vsa-item__trigger__icon--is-default:before {
  background-color: var(--vsa-text-color);
  content: '';
  height: 3px;
  position: absolute;
  top: 10px;
  transition: all 0.13333s ease-in-out;
  width: 30px;
}

.vsa-list >>> .vsa-item__trigger__icon--is-default:before {
  left: 0;
  transform: rotate(45deg) translate3d(8px, 22px, 0);
  transform-origin: 100%;
}

.vsa-list >>> .vsa-item__trigger__icon--is-default:after {
  transform: rotate(-45deg) translate3d(-8px, 22px, 0);
  right: 0;
  transform-origin: 0;
}

.vsa-list >>> .vsa-item__trigger[aria-expanded='true'] .vsa-item__trigger__icon--is-default:before {
  transform: rotate(45deg) translate3d(14px, 14px, 0);
}

.vsa-list >>> .vsa-item__trigger[aria-expanded='true'] .vsa-item__trigger__icon--is-default:after {
  transform: rotate(-45deg) translate3d(-14px, 14px, 0);
}

.vsa-list >>> .vsa-item__trigger__icon {
  display: block;
  margin-left: auto;
  position: relative;
  transition: all 0.2s ease-in-out;
}

.vsa-list >>> .vsa-item__trigger:focus .vsa-item__trigger__icon--is-default:after,
.vsa-list >>> .vsa-item__trigger:focus .vsa-item__trigger__icon--is-default:before,
.vsa-list >>> .vsa-item__trigger:hover .vsa-item__trigger__icon--is-default:after,
.vsa-list >>> .vsa-item__trigger:hover .vsa-item__trigger__icon--is-default:before {
  background-color: var(--vsa-text-color);
}

.vsa-list >>> .vsa-item__trigger__content {
  color: var(--vsa-heading-color);
  font-size: 1.25rem;
}

.vsa-list >>> .vsa-item__content {
  margin: 0;
  padding: var(--vsa-content-padding);
}

.vsa-list >>> .vsa-item--is-active .vsa-item__heading,
.vsa-list >>> .vsa-item:not(:last-of-type) {
  border-bottom: var(--vsa-border);
}

.vsa-list >>> .vsa-collapse-enter-active,
.vsa-list >>> .vsa-collapse-leave-active {
  transition-property: opacity, height, padding-top, padding-bottom;
  transition-duration: 0.3s;
  transition-timing-function: ease-in-out;
}

.vsa-list >>> .vsa-collapse-enter,
.vsa-list >>> .vsa-collapse-leave-active {
  opacity: 0;
  height: 0;
  padding-top: 0;
  padding-bottom: 0;
  overflow: hidden;
}
</style>
