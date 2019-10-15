<template>
  <div>
    <h3 style="color:red; margin-left:50px">[INSIDE]</h3>
    <b-navbar toggleable="lg" type="dark" variant="info" class="bg-danger">
      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <nuxt-link to="/" style="color:white; padding:6px">All</nuxt-link>
          <nuxt-link
            :to="'/' + tag.slug"
            v-for="tag in tags.data"
            :key="tag.id"
            style="color:white; padding: 6px"
          >
            {{ tag.name }}</nuxt-link
          >
        </b-navbar-nav>

        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <b-nav-form>
            <nuxt-link to="/formulario" style="color:white; padding:6px"
              >Login</nuxt-link
            >
            <nuxt-link to="/dashboard" style="color:white; padding:6px"
              >Panel</nuxt-link
            >
          </b-nav-form>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
//  import card1 from '@/components/card1.vue'
import axios from 'axios'

export default {
  components: {
    //  card1
  },
  data() {
    return {
      tags: ''
    }
  },
  created() {
    this.getTags()
  },
  methods: {
    getTags() {
      const url = process.env.apiTags1
      axios
        .get(url)
        .then((response) => {
          this.tags = response
        })
        .catch(() => {
          alert('error')
        })
    }
  }
}
</script>
