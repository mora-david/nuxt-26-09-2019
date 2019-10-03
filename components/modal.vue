<template>
  <div>
    <b-modal :id="datacard1.id" title="BootstrapVue">
      <img :src="datacard1.image" alt />
      <h2 class="my-4">{{ datacard1.title }}</h2>
      <p>{{ datacard1.description }}</p>
    </b-modal>
  </div>
</template>

<script>
export default {
  props: ['datacard1']
}
</script>
