<template>
  <div>
    <b-navbar
      wrapper-class="container"
      class="box is-paddingless is-marginless"
    >
      <template slot="brand">
        <b-navbar-item tag="router-link" :to="{ path: '/' }">
          <b-button type="is-primary" class="title is-6">
            Open Archipelago
          </b-button>
        </b-navbar-item>
      </template>

      <template slot="end">
        <b-navbar-dropdown label="Select a Framework">
          <b-navbar-item tag="router-link" to="/laravel">
            Laravel
          </b-navbar-item>
          <b-navbar-item tag="router-link" to="/vue">
            Vue
          </b-navbar-item>
        </b-navbar-dropdown>
      </template>
    </b-navbar>

    <nuxt />
  </div>
</template>

<script>
import 'nuxt-buefy'
export default {
  data() {
    return {
      items: [
        {
          title: 'Home',
          icon: 'home',
          to: { name: 'index' }
        },
        {
          title: 'Inspire',
          icon: 'lightbulb',
          to: { name: 'inspire' }
        }
      ]
    }
  }
}
</script>
