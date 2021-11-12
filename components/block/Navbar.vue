<template>
  <div class="nav">
    <nav
      class="navbar header is-gray"
      role="navigation"
      aria-label="main navigation"
    >
      <div class="navbar-brand">
        <Logo />
        <div class="navbar-burger">
          <span />
          <span />
          <span />
        </div>
      </div>
    </nav>
  </div>
</template>

<script lang="ts">
import Logo from '../atom/Logo.vue'
import Vue from 'vue'
export default Vue.extend({
  name: 'Navbar',
  components: {
    Logo,
  },
})
</script>
