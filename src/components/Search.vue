<template>
  <div class="form-group">
    <input
      v-model="value"
      type="text"
      class="form-control"
      placeholder="Enter nickname user..."
      @keypress="onSubmit($event)"
    />
  </div>
</template>

<script>
  export default {
    name: 'Search',
    data: () => ({
      value: ''
    }),
    methods: {
      onSubmit (event) {
        if (event.key !== 'Enter') {
          return
        }

        // github.clearUsers()

        if (this.value.trim()) {
          // alert.hide()
          // github.search(value.trim())
        } else {
          // alert.show('Please, enter data user!')
        }
      }
    }
  }
</script>

<style scoped>

</style>
