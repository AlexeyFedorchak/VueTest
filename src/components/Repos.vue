<template>
  <div>
    <div class="card mb-3" v-for="rep in repos" :key="rep.id">
      <div class="card-body">
        <h5>
          <a
            :href="rep.html_url"
            target="_blank"
            rel="noopener noreferrer"
          >{{ rep.name }}</a>
        </h5>
      </div>
    </div>
  </div>

</template>

<script>
  import axios from 'axios'
  const CLIENT_ID = process.env.VUE_APP_CLIENT_ID
  const CLIENT_SECRET = process.env.VUE_APP_CLIENT_SECRET

  export default {
    name: 'Repos',
    data: () => ({
      repos: []
    }),
    async mounted () {
      let name = this.$route.params.id;
      axios.get(this.withCreds(`https://api.github.com/users/${name}/repos?per_page=5&`))
        .then((res) => {
          this.repos = res.data
        })
    },
    methods: {
      withCreds (url) {
        return `${url}client_id=${CLIENT_ID}&client_secret=${CLIENT_SECRET}`
      },
    }
  }
</script>

<style scoped>

</style>
