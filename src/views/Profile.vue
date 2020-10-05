<template>
  <div class="container pt-4">
    <router-link to='/' class='btn btn-link'>Return to main page</router-link>

    <div class="card mb-4">
      <div class="card-body">
        <div class="row">
          <div class="col-sm-3 text-center">
            <img
              :src="profile.avatar_url"
              :alt="profile.name"
              style="width: 150px"
            />
            <h1>{{profile.name}}</h1>
            <div v-if="profile.location">
              <p>Location: {{ profile.location }}</p>
            </div>
          </div>
          <div class="col text-left">
            <div v-if="profile.bio">
              <h3>BIO</h3>
              <p>{{profile.bio}}</p>
            </div>
            <a
              :href="profile.html_url"
              target='_blank'
              rel="noopener noreferrer"
              class='btn btn-dark mb-2'
            >Open profile</a>
            <ul>
              <li v-if="profile.login">
                <strong>Username: </strong> {{profile.login}}
              </li>
              <li v-if="profile.company">
                <strong>Company: </strong> {{profile.company}}
              </li>
              <li v-if="profile.blog">
                <strong>Website: </strong> {{profile.blog}}
              </li>
            </ul>

            <div class="badge badge-primary mr-1">Followers: {{ profile.followers }}</div>
            <div class="badge badge-success mr-1">Followers: {{ profile.following }}</div>
            <div class="badge badge-info mr-1">Repositories: {{ profile.public_repos }}</div>
            <div class="badge badge-dark mr-1">Gists: {{ profile.public_gists }}</div>
          </div>
        </div>
      </div>
    </div>
    <Repos :repos="profile.repos" />
  </div>

</template>

<script>
  import axios from 'axios'
  import Repos from "../components/Repos"

  const CLIENT_ID = process.env.VUE_APP_CLIENT_ID
  const CLIENT_SECRET = process.env.VUE_APP_CLIENT_SECRET

  export default {
    name: 'Profile',
    data: () => ({
      profile: {},
    }),
    components: {
      Repos
    },
    mounted () {
      let name = this.$route.params.id
      axios.get(this.withCreds(`https://api.github.com/users/${name}?`))
        .then((res) => {
          this.profile = res.data
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
