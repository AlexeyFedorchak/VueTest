<template>
  <nav class="navbar navbar-dark bg-dark navbar-expand-lg">
    <div class="navbar-brand">
      Github Search
    </div>
    <ul class="navbar-nav">
      <li class="nav-item">
        <router-link exact to='/' class="nav-link">Home</router-link>
      </li>
      <li class="nav-item">
        <router-link to='/about' class="nav-link">Info</router-link>
      </li>
    </ul>
  </nav>
</template>

<script>
  export default {
    name: 'Navbar'
  }
</script>

<style scoped>

</style>
