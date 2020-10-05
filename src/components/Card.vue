<template>
  <div class='card'>
    <img :src='user.avatar_url' :alt='user.login' class="card-img-top"/>
    <div class="card-body">
      <h5 class='card-title'>{{ user.login }}</h5>
      <router-link :to='`/profile/${user.login}`' class='btn btn-dark'>Open</router-link>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Card',
    props: {
      user: {}
    }
  }
</script>

<style scoped>

</style>
