<template>
  <div id="app">
    <AppHeader @setPage="setPage" />
    <AppBody :page="page" />
    <AppFooter />
  </div>
</template>

<script>
import AppHeader from './components/AppHeader.vue'
import AppBody from './components/AppBody.vue'
import AppFooter from './components/AppFooter.vue'

export default {
  name: 'App',
  data() {
    return {
      page: 'fields'
    }
  },
  components: {
    AppHeader,
    AppBody,
    AppFooter
  },
  methods: {
    setPage(page) {
      this.page = page
      localStorage.setItem('page', JSON.stringify(this.page))
    }
  },
  mounted() {
    if (localStorage.getItem('page')) {
      this.page = JSON.parse(localStorage.getItem('page'))
    }
  }
}
</script>

<style lang="scss">
body {
  margin: 0;
  padding: 0;
}

#app {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.block {
  max-width: 70%;
  margin: 0 auto;
}
</style>
