<template>
  <div>
    <div class="container" id="padre1">
      <h3 class="text-center my-5">Real news, curated by real humans</h3>
      <p class="text-center my-5">
        Packed with the trends and links you need to be smart, informed, and
        ahead of the curve
      </p>
      <div style="display:flex; flex-wrap:wrap; width:90%">
        <div v-for="datacard in datacardsSub" :key="datacard.id" class style>
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
              <!-- <input type="email" :id="'id' + datacard.id" /> -->
              <b-button
                @click.prevent="
                  //  suscribe(datacard.id)
                  $bvModal.show(datacard.id)
                "
                href="#"
                variant="primary"
                >Subscribe</b-button
              >
            </b-card>
          </div>
          <modal :datacard1="datacard" :metos1="suscribe"></modal>
        </div>
      </div>
    </div>
    <div class="container">
      <div class="my-5">
        <h2 class="text-center">Up-and-Coming</h2>
        <p class="text-center">
          if these newsletter reach their goals (or get sponsorship),we´ll bring
          on expert writers and launch them. Vote for all your favorites
        </p>
      </div>
      <div style="display:flex; flex-wrap:wrap; width:90%">
        <div v-for="datacard in datacardsTar" :key="datacard.id">
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
              <!-- <input type="email" :id="'id' + datacard.id" /> -->
              <div class="progress my-3">
                <div
                  class="progress-bar progress-bar-striped"
                  role="progressbar"
                  :style="
                    'width:' +
                      getporcentaje(datacard.subscribed, datacard.target) +
                      '%'
                  "
                  aria-valuenow="10"
                  aria-valuemin="0"
                  aria-valuemax="100"
                ></div>
              </div>
              <b-button
                @click.prevent="
                  // suscribe(datacard.id)
                  $bvModal.show(datacard.id)
                "
                href="#"
                variant="primary"
                class="bg-danger"
                >Subscribe</b-button
              >
            </b-card>
          </div>
          <modal :datacard1="datacard" :metos1="suscribe"></modal>
          <!-- <modal :datacard1="datacard" :metos1="prueba1"></modal> -->
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
    prueba1() {
      alert('funciono')
    },
    getporcentaje(num1, num2) {
      const result = num1 / num2
      return result * 100
    },
    progresprueba() {
      return 50
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
