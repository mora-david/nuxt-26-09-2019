<template>
  <div>
    <div class="container">
      <div
        v-for="datacard in datacardsTar"
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
            <b-card-text>target:{{ datacard.target }}</b-card-text>
            <b-card-text>Subscribed:{{ datacard.subscribed }}</b-card-text>
            <input type="email" :id="'id' + datacard.id" />
            <b-button
              @click.prevent="
                suscribe(datacard.id)
                $bvModal.show(datacard.id)
              "
              href="#"
              variant="primary"
              >Agregar Email</b-button
            >
          </b-card>
        </div>
        <modal :datacard1="datacard"></modal>
      </div>
    </div>
    <div>
      <h2 style="padding-left:650px">Up-and-Coming</h2>
      <p style="padding-left:300px">
        if these newsletter reach their goals (or get sponsorship),we´ll bring
        on expert writers and launch them. Vote for all your favorites
      </p>
      <div class="container">
        <div
          v-for="datacard in datacardsSub"
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
              <b-card-text>target:{{ datacard.target }}</b-card-text>
              <b-card-text>Subscribed:{{ datacard.subscribed }}</b-card-text>
              <input type="email" :id="'id' + datacard.id" />
              <b-button
                @click.prevent="
                  suscribe(datacard.id)
                  $bvModal.show(datacard.id)
                "
                href="#"
                variant="primary"
                >Agregar Email</b-button
              >
            </b-card>
          </div>
          <modal :datacard1="datacard"></modal>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapMutations } from 'vuex'
//  import card1 from '@/components/card1.vue'
import axios from 'axios'
import modal from '@/components/modal.vue'

export default {
  components: {
    modal
  },
  data() {
    return {
      datacards: '',
      datacardsSub: '',
      datacardsTar: '',
      infos: { email: 'dd', newsletter_id: '1' },
      prueba: { name: 'jorge' }
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
