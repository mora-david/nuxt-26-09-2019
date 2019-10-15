<template>
  <div>
    <navbar></navbar>
    <h1>probando layout</h1>
    <nuxt />
    <footer1></footer1></div
></template>

<script>
import navbar from '@/components/navbar.vue'
import footer1 from '@/components/footer1.vue'
export default {
  components: {
    navbar,
    footer1
  }
}
</script>
