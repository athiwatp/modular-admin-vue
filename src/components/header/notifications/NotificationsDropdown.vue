<template>

  <li class="notifications new" :class="{open: show}">
    <a href="#" data-toggle="dropdown" v-on:click.stop.prevent="toggle()">
      <i :class="['fa', notificationIcon]"></i>
      <sup>
        <span class="counter">{{ numberOfNotifications }}</span>
      </sup>
    </a>
    <div class="dropdown-menu notifications-dropdown-menu">
      <ul class="notifications-container">
        <slot></slot>
      </ul>
      <footer>
        <ul>
          <li>
            <a v-bind:href="allNotificationsLink">{{ allNotificationsText }}</a>
          </li>
        </ul>
      </footer>
    </div>
  </li>

</template>

<script>
  export default {
    name: 'modular-admin-notifications-dropdown',
    replace: true,
    data () {
      return {
        show: false
      }
    },
    props: {
      notificationIcon: {
        type: String,
        default: ''
      },
      numberOfNotifications: {
        type: String,
        default: 0
      },
      allNotificationsLink: {
        type: String,
        default: '#'
      },
      allNotificationsText: {
        type: String,
        default: 'View All'
      }
    },
    methods: {
      toggle () {
        this.show = !this.show
        if (this.show) {
          this.$root.$emit('maVue::shown::notificationsDropdown', this)
        } else {
          this.$root.$emit('maVue::hidden::notificationsDropdown')
        }
      }
    },
    created: function () {
      this.$root.$on('maVue::hide::notificationsDropdown', () => {
        this.show = false
      })
      this.$root.$on('maVue::shown::notificationsDropdown', (element) => {
        if (element !== this) {
          this.show = false
        }
      })
      this.$root.$on('maVue::shown::profileDropdown', () => {
        this.show = false
      })
    }
  }

</script>