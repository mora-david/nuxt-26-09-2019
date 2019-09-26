<template>
  <div>
    <div>
      <div class="container" style="margin:50px">
        <div v-for="tag in categories1" :key="tag.slug" class="container">
          <div>
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
                @click.prevent="suscribe(tag.id)"
                href="#"
                variant="primary"
                >Agregar Email</b-button
              >
            </b-card>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  components: {},
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
