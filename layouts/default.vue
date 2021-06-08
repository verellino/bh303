<template>
  <div class="wrapper">
    <Header />
    <Sidenav />
    <nuxt />
  </div>
</template>

<script>
export default {        
    computed: {
      isSidebar() {
          return this.$store.getters['nav/toggleSidebar']
      }
    },
    watch: {
      '$route': function() {
          if (process.client && this.isSidebar && window.innerWidth < 768) {
              this.$store.dispatch('nav/toggleSidebar')
          }
      }
  }
}
</script>