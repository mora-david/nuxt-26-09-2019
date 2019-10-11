<template>
  <div>
    <b-modal :id="datacard1.id" title="BootstrapVue">
      <img :src="datacard1.image" alt />
      <h2 class="my-4">{{ datacard1.title }}</h2>
      <p>{{ datacard1.description }}</p>
      <input type="email" :id="'id' + datacard1.id" />
      <button type="button" @click.prevent="metos1(datacard1.id)">Send</button>
    </b-modal>
  </div>
</template>

<script>
export default {
  methods: {
    meto1() {
      alert()
    }
  },
  props: ['datacard1', 'metos1']
}
</script>
