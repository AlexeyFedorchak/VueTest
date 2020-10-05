<template>
  <div class="container pt-4">
    <div class="form-group">
      <input
              v-model="value"
              type="text"
              class="form-control"
              placeholder="Enter nickname user..."
              @keypress="onSubmit($event)"
      />
    </div>
    <div class='row'>
      <p v-if="loading" class='text-center'>Download...</p>
      <div v-else class="col-sm-4 mb-4" v-for="user in users" :key="user.id">
        <ItemCard :user="user"/>
      </div>
    </div>
  </div>
</template>

<script>
import ItemCard from '../components/Card'
import axios from 'axios'

const CLIENT_ID = process.env.VUE_APP_CLIENT_ID
const CLIENT_SECRET = process.env.VUE_APP_CLIENT_SECRET

export default {
  name: 'Home',
  data: () => ({
    value: 'OleksiiFedorchak',
    loading: false,
    users: []
  }),
  components: {
    ItemCard
  },
  mounted () {
    this.sendRequest()
  },
  methods: {
    onSubmit (event) {
      if (event.key !== 'Enter') {
        return
      }
      this.sendRequest()
    },

    withCreds (url) {
      return `${url}client_id=${CLIENT_ID}&client_secret=${CLIENT_SECRET}`
    },

    sendRequest () {
      if (this.value.trim()) {
        this.loading = true;
        axios.get(this.withCreds(`https://api.github.com/search/users?q=${this.value}&`))
          .then((res) => {
            this.users = res.data.items
          })
          .finally( () => {
            this.loading = false;
          })
      } else {
        // alert
      }
    }
  }
}
</script>
