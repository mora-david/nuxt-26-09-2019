<template>
  <div class="container mt-5">
    <hr />
    <b-form @submit.prevent="onSubmit">
      <b-form-group
        id="input-group-1"
        label="Email address:"
        label-for="input-1"
      >
        <b-form-input
          id="input-1"
          v-model="form.email"
          type="email"
          required
          placeholder="Enter email"
        ></b-form-input>
      </b-form-group>
      <b-form-group id="input-group-1" label="Password:" label-for="input-1">
        <b-form-input
          id="input-1"
          v-model="form.password"
          type="password"
          required
        >
        </b-form-input>
      </b-form-group>
      <b-button type="submit" variant="primary">
        Submit
      </b-button>
    </b-form>
    <div v-if="!valor">
      Esto es verdadero
    </div>
    <nuxt-link to="prueba">Prueba</nuxt-link>
  </div>
</template>

<script>
import { mapMutations } from 'vuex'
import axios from 'axios'
export default {
  middleware: 'loggedIn',
  data() {
    return {
      form: {
        email: '',
        password: ''
      },
      valor: false
    }
  },
  created() {},
  methods: {
    ...mapMutations(['login']),
    onSubmit() {
      const dire = 'https://newsletters.academlo.com/api/v1/auth/login'
      const data = this.form
      axios
        .post(dire, data)
        .then((response) => {
          this.login(response)
          alert('logeado')
        })
        .catch(() => {
          alert('error')
        })
      // alert('La sesión se inició correctamente')
    }
  }
}
</script>
