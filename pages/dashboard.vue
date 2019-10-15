<template>
  <div>
    <div class="container my-5">
      <table class="table">
        <thead class="thead-dark">
          <tr>
            <th scope="col">id</th>
            <th scope="col">Title</th>
            <th scope="col">Subscribed</th>
            <th scope="col">Target</th>
            <th scope="col"></th>
            <th scope="col">Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="datacard in datacards.data" :key="datacard.id">
            <th scope="row">{{ datacard.id }}</th>
            <td>{{ datacard.title }}</td>
            <td>{{ datacard.subscribed }}</td>
            <td>{{ datacard.target }}</td>
            <td><modal-add-new :datacards2="datacard"></modal-add-new></td>
            <td>
              <button @click.prevent="delatenew(datacard.id)">Eliminar</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="container" style="display:flex">
      <h5>titulo</h5>
      <input type="text" v-model="form.title" />
      <h5>descripción</h5>
      <input type="text" v-model="form.description" />
      <h5>target</h5>
      <input type="text" v-model="form.target" />
      <button @click.prevent="addnew">Agregar</button>
    </div>
  </div>
</template>

<script>
import { mapMutations } from 'vuex'
//  import card1 from '@/components/card1.vue'
import axios from 'axios'
import modalAddNew from '@/components/modalAddNew.vue'
export default {
  middleware: 'authenticated',
  layout: 'withlog',
  components: { modalAddNew },
  data() {
    return {
      datacards: '',
      datacardsSub: '',
      datacardsTar: '',
      infos: { email: 'dd', newsletter_id: '1' },
      prueba: { name: 'jorge' },
      form: { title: '', description: '', target: '' }
    }
  },
  created() {
    this.getNews()
  },
  methods: {
    ...mapMutations(['neim']),
    suscribe(param) {
      const url = 'https://newsletters.academlo.com/api/v1/users'
      const data = {
        email: document.getElementById('id' + param).value,
        newsletter_id: param
      }
      axios
        .post(url, data)
        .then((response) => {})
        .catch(() => {
          alert('error')
        })
    },
    addnew() {
      const url = 'https://newsletters.academlo.com/api/v1/newsletters'
      const data = this.form
      axios
        .post(url, data)
        .then((response) => {
          this.form.title = ''
          this.form.description = ''
          this.form.target = ''
        })
        .catch(() => {
          alert('error')
        })
    },
    delatenew(id) {
      const url = 'https://newsletters.academlo.com/api/v1/newsletters/' + id
      axios
        .delete(url)
        .then((response) => {})
        .catch(() => {
          alert('error')
        })
    },
    prueba1() {
      alert('funciono')
    },
    filter(newsletters) {
      const approved = newsletters.filter(function(newsletter) {
        return newsletter.subscribed >= newsletter.target
      })
      console.log(approved)
      return approved
    },
    getNews() {
      const url = process.env.apiUrl
      axios
        .get(url)
        .then((response) => {
          this.datacards = response
          this.datacardsSub = this.filter(this.datacards.data)
          this.datacardsTar = this.datacards.data.filter(
            (tar) => tar.subscribed < tar.target
          )
        })
        .catch(() => {
          alert('error')
        })
    },
    getTags() {
      const url = process.env.apiUrl
      axios
        .get(url)
        .then((response) => {
          this.datacards = response
          this.datacardsSub = this.filter(this.datacards.data)
        })
        .catch(() => {
          alert('error')
        })
    }
  }
}
</script>
