<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="info">
      <b-navbar-brand href="#">NavBar</b-navbar-brand>

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
            <b-form-input
              size="sm"
              class="mr-sm-2"
              placeholder="Search"
            ></b-form-input>
            <b-button size="sm" class="my-2 my-sm-0" type="submit"
              >Search</b-button
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
