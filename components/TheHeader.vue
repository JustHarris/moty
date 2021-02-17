<template>
  <div data-sw-path="header">
    <!-- Duplicate elements to match header height and push main content down -->
    <div class="opacity-0" :style="{ height: header.logoHeight + 'px' }">
      <ThePromoBar v-if="header.showPromo" text="|" :hidden="header.hideOnScroll && hideHeader" />
      <div class="my-3">
        <span v-if="logoSrc" :style="{ height: header.logoHeight + 'px' }" class="block"></span>
        <span v-else class="text-3xl sm:text-4xl">|</span>
      </div>
    </div>

    <!-- Full screen nav for small screens -->
    <TheMobileNav v-if="mobileNavIsVisible" :menu-items="menu.items" />

    <!-- Main header -->
    <div class="z-40 fixed top-0 w-full">
      <ThePromoBar
        v-if="header.showPromo"
        :url="header.promoUrl"
        :text="header.promoText || '[ Promotional text ]'"
        :hidden="header.hideOnScroll && hideHeader"
      />

      <div class="w-full fixed transform translate-y-0 transition-all ease-in-out duration-200">
        <header
          class="z-40 shadow-md transition-all duration-300 ease-in-out"
          :class="[
            'border-b-2 bg-moty-darker text-moty-lightest border-transparent',
            { 'transform -translate-y-full': header.hideOnScroll && hideHeader }
          ]"
        >
          <div class="relative container flex items-stretch justify-between items-stretch z-20">
            <!-- Logo -->
            <div class="py-3 lg:w-1/4">
              <NuxtLink :to="resolveUrl({ type: 'home' })">
                <MotyLogo
                  class="inline-block w-auto"
                  :height="header.logoHeight"
                  :style="{ height: header.logoHeight + 'px' }"
                />
              </NuxtLink>
            </div>

            <!-- Main nav menu -->
            <nav v-if="menu" class="w-full font-body_bold text-sm lg:w-auto hidden lg:flex">
              <ul class="flex justify-center">
                <li v-for="item in menu.items" :key="item.name" class="sw-nav-link-wrapper mb-0">
                  <NuxtLink
                    :to="resolveUrl(item)"
                    :title="item.description"
                    class="sw-nav-link relative flex items-center h-full px-5 pt-1 rounded-none border-transparent border-b-4"
                    @click.native="megaNavIsEnabled = false"
                    @mouseleave.native="resetMegaNav"
                  >
                    <span class="relative">
                      {{ item.name }}
                    </span>
                  </NuxtLink>
                  <!-- Show mega nav if item has child items -->
                  <div
                    v-if="item && item.items && megaNavIsEnabled"
                    class="mega-nav fade-in hidden absolute left-0 right-0 min-h-full"
                  >
                    <MegaNav :items="item.items" @click="resetMegaNav" />
                  </div>
                </li>
              </ul>
            </nav>
            <!-- END Main nav menu -->

            <!-- Action menu -->
            <div class="flex flex-row items-center justify-end -mr-2 lg:w-1/4">
              <MotyButton
                :links="[
                  {
                    link: '/entrar',
                    title: 'Entrar',
                    label: 'Entrar',
                    style: 'button_primary_adjusted'
                  }
                ]"
              ></MotyButton>
              <!-- Mobile nav toggle -->
              <button
                :class="{ 'is-active': mobileNavIsVisible }"
                class="hamburger hamburger--squeeze h-8 p-1 ml-2 rounded lg:hidden"
                type="button"
                @click="setMobileNavVisibility"
              >
                <span class="hamburger-box">
                  <span class="hamburger-inner"></span>
                </span>
              </button>
            </div>
          </div>
          <div class="relative w-full z-40 h-0">
            <div
              class="absolute inset-0 w-full top-1 border-b-4 border-moty-oklight h-0"
              :class="[{ ' hidden': header.hideOnScroll && hideHeader }]"
            ></div>
          </div>
        </header>
      </div>
    </div>
    <!-- END Main header -->
  </div>
</template>

<script>
// Helpers
import { mapState } from 'vuex'
// import get from 'lodash/get'
import MotyLogo from '../static/assets/logo-base.svg'
import MotyButton from './MotyButton'

export default {
  name: 'TheHeader',

  components: {
    MotyLogo,
    MotyButton
  },

  fetch() {
    const { $swell } = this

    // Get menu ID
    const menuId = $swell.settings.get('header.menu', 'header')

    // Set component data
    this.header = $swell.settings.get('header', {})
    this.menu = $swell.settings.menus(menuId)
    this.storeName = $swell.settings.get('store.name', 'ORIGIN')
    this.logoSrc = $swell.settings.get('header.logo.file.url')
  },

  data() {
    return {
      header: {},
      menu: {},
      storeName: null,
      logoSrc: null,
      mounted: false,
      megaNavIsEnabled: true,
      mobileNavIsVisible: false,
      hideHeader: false,
      lastScrollPos: 0,
      isScrolled: false,
      scrollRAF: null
    }
  },

  computed: {
    ...mapState(['cart'])
  },

  watch: {
    $route() {
      // Close mega/mobile nav menu when the page changes
      this.hideHeader = false
      this.setMobileNavVisibility(false)
    }
  },

  mounted() {
    this.setScrollListener(true)
  },

  beforeDestroy() {
    this.setScrollListener(false)
    cancelAnimationFrame(this.scrollRAF)
  },

  methods: {
    setMobileNavVisibility(value) {
      if (typeof value === 'boolean') {
        // Explicitly set visibility
        this.mobileNavIsVisible = value
      } else {
        // Toggle visibility
        this.mobileNavIsVisible = !this.mobileNavIsVisible
      }

      // Ensure the header is visible when mobile nav is open
      if (this.mobileNavIsVisible) {
        this.setScrollListener(false)
      } else {
        this.setScrollListener(true)
      }
    },

    setHeaderVisibility() {
      this.isScrolled = false
      // Check how far page has scrolled
      const currentScrollPosition = window.pageYOffset || document.documentElement.scrollTop
      if (currentScrollPosition < 0) return

      // Stop executing this function if the difference between
      // current scroll position and last scroll position is less than some offset
      if (Math.abs(currentScrollPosition - this.lastScrollPos) < 50) return

      this.hideHeader = currentScrollPosition > this.lastScrollPos
      this.lastScrollPos = currentScrollPosition
    },

    handleScroll() {
      if (!this.isScrolled) {
        this.isScrolled = true
        this.scrollRAF = requestAnimationFrame(this.setHeaderVisibility)
      }
    },

    setScrollListener(value) {
      // Ignore if hide on scroll is disabled in settings
      if (!this.header.hideOnScroll) return

      if (value) {
        window.addEventListener('scroll', this.handleScroll)
      } else {
        window.removeEventListener('scroll', this.handleScroll)
        this.hideHeader = false
      }
    },

    resetMegaNav(event) {
      // When a link is clicked, make the mega nav disappear
      if (event.type === 'click') {
        this.megaNavIsEnabled = false
      }

      // Wait for the hover state to be broken then re-enable the nav
      setTimeout(() => {
        this.megaNavIsEnabled = true
      }, 10)
    }
  }
}
</script>

<style lang="postcss">
.sw-nav-link {
  &:focus,
  &.nuxt-link-active {
    @apply text-moty-okmed;
  }
}

.mega-nav:hover,
.sw-nav-link-wrapper a:hover + .mega-nav {
  @apply block;
}

.hamburger {
  @apply cursor-pointer;
}

.hamburger-box {
  @apply relative inline-block w-6 h-6;
}

.hamburger-inner {
  @apply block -mt-px top-1/2;

  &,
  &:before,
  &:after {
    @apply absolute w-6 h-2px bg-current rounded;
  }

  &:before,
  &:after {
    content: '';
    display: block;
  }

  &:before {
    top: -8px;
  }

  &:after {
    bottom: -8px;
  }
}

.hamburger--squeeze .hamburger-inner {
  transition-duration: 0.075s;
  transition-timing-function: cubic-bezier(0.55, 0.055, 0.675, 0.19);
}
.hamburger--squeeze .hamburger-inner::before {
  transition: top 0.075s 0.12s ease, opacity 0.075s ease;
}
.hamburger--squeeze .hamburger-inner::after {
  transition: bottom 0.075s 0.12s ease, transform 0.075s cubic-bezier(0.55, 0.055, 0.675, 0.19);
}

.hamburger--squeeze.is-active .hamburger-inner {
  transform: rotate(45deg);
  transition-delay: 0.12s;
  transition-timing-function: cubic-bezier(0.215, 0.61, 0.355, 1);
}
.hamburger--squeeze.is-active .hamburger-inner::before {
  top: 0;
  opacity: 0;
  transition: top 0.075s ease, opacity 0.075s 0.12s ease;
}
.hamburger--squeeze.is-active .hamburger-inner::after {
  bottom: 0;
  transform: rotate(-90deg);
  transition: bottom 0.075s ease, transform 0.075s 0.12s cubic-bezier(0.215, 0.61, 0.355, 1);
}
</style>
