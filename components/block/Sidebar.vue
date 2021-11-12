<template>
  <div class="sidebar">
    <div class="search-bar">
      <img src="~assets/Search.svg" alt="" />
      <input type="text" placeholder="Search..." />
    </div>
    <ul class="sidebar-menu">
      <li class="sidebar-links">
        <nuxt-link to="/welcome" active-class="active-tab" class=""
          >Welcome</nuxt-link
        >
      </li>
      <li class="sidebar-links">
        <nuxt-link to="/data" active-class="active-tab">Data import</nuxt-link>
      </li>
      <li class="sidebar-links">
        <nuxt-link to="/import" active-class="active-tab"
          >Import requests</nuxt-link
        >
      </li>
    </ul>
    <ul class="sidebar-menu">
      <li class="sidebar-links">
        <nuxt-link to="/welcome" active-class="active-tab" class=""
          >Self onboarding process</nuxt-link
        >
      </li>
      <li class="sidebar-links">
        <nuxt-link to="/data" active-class="active-tab">Change plan</nuxt-link>
      </li>
      <li class="sidebar-links" style="padding-left: 24px">
        <nuxt-link style="display: flex" to="/import" active-class="active-tab"
          ><img style="margin-right: 10px" src="~assets/arrow.svg" alt="" /> Evo
          University</nuxt-link
        >
      </li>
      <li class="sidebar-links" style="padding-left: 24px">
        <nuxt-link style="display: flex" to="/import" active-class="active-tab"
          >Portal & adding stats</nuxt-link
        >
      </li>
    </ul>
    <div class="sidebar-footer">
      <img style="margin-right: 10px" src="~assets/arrow-left.svg" alt="" />
      <p>collapse</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      expandOnHover: false,
      expandWithDelay: false,
      mobile: 'reduce',
      reduce: false,
    }
  },
}
</script>
