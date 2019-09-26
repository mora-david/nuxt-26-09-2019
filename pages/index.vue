<template>
  <div>
    <navbar></navbar>
    <div class="container">
      <div
        v-for="datacard in datacards.data"
        :key="datacard.id"
        class="container"
      >
        <div>
          <b-card
            :title="datacard.title"
            :img-src="datacard.image"
            img-alt="Image"
            img-top
            tag="article"
            style="max-width: 20rem;"
            class="mb-2"
          >
            <b-card-text>{{ datacard.description }}</b-card-text>

            <input type="email" :id="'id' + datacard.id" />
            <b-button
              @click.prevent="suscribe(datacard.id)"
              href="#"
              variant="primary"
              >Agregar Email</b-button
            >
          </b-card>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
//  import card1 from '@/components/card1.vue'
import axios from 'axios'

export default {
  components: {},
  data() {
    return {
      datacards: '',
      infos: { email: '', newsletter_id: '1' }
    }
  },
  created() {
    this.getNews()
  },
  methods: {
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
    getNews() {
      const url = process.env.apiUrl
      axios
        .get(url)
        .then((response) => {
          this.datacards = response
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
        })
        .catch(() => {
          alert('error')
        })
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
