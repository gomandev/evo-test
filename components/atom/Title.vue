<template>
  <div class="title" style="margin-top: 15px">
    <h1><slot /></h1>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  name: 'Title',
})
</script>
