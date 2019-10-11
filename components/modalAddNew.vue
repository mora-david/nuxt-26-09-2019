<template>
  <div>
    <div>
      <b-button @click.prevent="$bvModal.show(datacards2.id)">Editar</b-button>
      <b-modal :id="datacards2.id" title="editar">
        <input type="text" v-model="form.title" />
        <input type="text" v-model="form.description" />
        <input type="text" v-model="form.target" />
        <button @click.prevent="edition(datacards2.id)">soy botón</button>
      </b-modal>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      form: {
        title: this.datacards2.title,
        description: this.datacards2.description,
        targert: this.datacards2.target
      }
    }
  },
  props: ['datacards2'],
  methods: {
    edition(id) {
      const url = 'https://newsletters.academlo.com/api/v1/newsletters/' + id
      axios
        .patch(url, this.form)
        .then((response) => {})
        .catch(() => {
          alert('error')
        })
    }
  }
}
</script>
