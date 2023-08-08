<template>
  <div class="body">
    <AppFields v-if="page === 'fields'" :person="person" @updatePersonData="updatePersonData" />
    <AppPreview v-else :person="person" />
  </div>
</template>

<script>
import AppFields from './AppFields.vue'
import AppPreview from './AppPreview.vue'

export default {
  name: 'AppBody',
  data() {
    return {
      person: {
        name: 'Сергей',
        age: 30,
        children: []
      }
    }
  },
  props: {
    page: {
      type: String,
      default: 'fields'
    }
  },
  components: {
    AppFields,
    AppPreview
  },
  methods: {
    updatePersonData(data) {
      this.person = JSON.parse(JSON.stringify(data))
      localStorage.setItem('person', JSON.stringify(this.person))
    }
  },
  mounted() {
    if (localStorage.getItem('person')) {
      this.person = JSON.parse(localStorage.getItem('person'))
    }
  }
}
</script>

<style scoped lang="scss">
@import "@/assets/scss/main.scss";

.body {
  width: 50%;
  margin: 0 auto 30px;
}
</style>