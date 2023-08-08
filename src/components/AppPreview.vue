<template>
  <div class="preview">
    <div class="preview__block">
      <div class="preview__title">Персональные данные</div>
      <div class="preview__data">{{ person.name }}, {{ person.age }} лет</div>
    </div>

    <div class="preview__block">
      <div class="preview__title">Дети</div>
      <div class="preview__data">
        <div v-for="child in person_data.children" :key="child.id" class="preview__child">
          {{ child.name }}, {{ child.age }} лет
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AppPreview',
  data() {
    return {
      person_data: {}
    }
  },
  props: {
    person: {
      type: Object,
      default: () => { }
    }
  },
  mounted() {
    this.person_data = JSON.parse(JSON.stringify(this.person))
  },
  watch: {
    person() {
      this.person_data = this.person
    }
  }
}
</script>

<style scoped lang="scss">
@import "@/assets/scss/main.scss";

.preview {
  display: flex;
  flex-direction: column;
  gap: 60px;

  &__block {
    display: flex;
    flex-direction: column;
    gap: 20px;
  }

  &__title {
    @include montserrat-normal-16;
    color: $colors-second-black;
  }

  &__data {
    display: flex;
    flex-direction: column;
    gap: 20px;
  }

  &__child {
    max-width: max-content;
    padding: 10px 20px;
    @include montserrat-normal-16;
    /*@TODO заменить*/
    color: $colors-second-black;
    border-radius: 5px;
    background: $colors-gray-l;
  }
}
</style>