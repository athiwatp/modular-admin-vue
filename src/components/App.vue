<template>
  <div class="main-wrapper" v-on:click="bodyClick">
    <div class="app" :class="{'sidebar-fixed': fixedSidebar, 'footer-fixed': fixedFooter, 'sidebar-open': sidebarOpen}">
      <slot></slot>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'modular-admin-app',
    data () {
      return {
        sidebarOpen: false
      }
    },
    props: {
      fixedSidebar: {
        type: Boolean,
        default: false
      },
      fixedFooter: {
        type: Boolean,
        default: false
      }
    },
    methods: {
      bodyClick () {
        this.$root.$emit('maVue::hide::notificationsDropdown')
        this.$root.$emit('maVue::hide::profileDropdown')
        this.$root.$emit('maVue::hide::sidebar')
      }
    },
    created () {
      this.$root.$on('maVue::collapseSidebar', () => {
        this.sidebarOpen = !this.sidebarOpen
      })

      this.$root.$on('maVue::hide::sidebar', () => {
        this.sidebarOpen = false
      })
    }
  }
</script>