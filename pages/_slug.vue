<template>
  <div>
    <div>
      <div class="d-flex p-2 bd-highlight" style="margin:50px">
        <div v-for="tag in categories1" :key="tag.slug" class>
          <b-card
            :title="tag.title"
            :img-src="tag.image"
            img-alt="Image"
            img-top
            tag="article"
            style="max-width: 20rem;"
            class="mb-2"
          >
            <b-card-text>{{ tag.description }} {{ tag.id }}</b-card-text>

            <input type="email" :id="'id' + tag.id" />
            <b-button
              @click.prevent="
                suscribe(tag.id)
                $bvModal.show(tag.id)
              "
              href="#"
              variant="primary"
              >Agregar Email</b-button
            >
          </b-card>
          <modal :datacard1="tag"></modal>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import modal from '@/components/modal.vue'

export default {
  components: { modal },
  data() {
    return {
      categories: '',
      categories1: ''
    }
  },
  created() {
    this.getTagsNews()
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
    getTagsNews() {
      const url =
        process.env.apiTags1 +
        '/' +
        this.$root.$route.params.slug +
        '?include=newsletters'
      axios
        .get(url)
        .then((response) => {
          this.categories = response
          this.categories1 = this.categories.data.newsletters
        })
        .catch(() => {
          alert('error')
        })
    }
  }
}
</script>
