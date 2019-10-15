<template>
  <div>
    <div>
      <b-button @click.prevent="$bvModal.show(datacards2.id)">Editar</b-button>
      <b-modal :id="datacards2.id" title="Editar">
        <div>
          <h5>Título</h5>
          <input type="text" v-model="form.title" class="mb-2" />
        </div>
        <div>
          <h5>Descripción</h5>
          <input type="text" v-model="form.description" class="mb-2" />
        </div>
        <div>
          <h5>Target</h5>
          <input type="text" v-model="form.target" class="mb-2" />
        </div>
        <button @click.prevent="edition(datacards2.id)">Envíar</button>
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
