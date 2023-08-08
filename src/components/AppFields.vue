<template>
  <div class="fields">
    <div class="fields__field">
      <div class="fields__title">Персональные данные</div>
      <div class="fields__input">
        <span>Имя</span>
        <input type="text" v-model="person_data.name">
      </div>
      <div class="fields__input">
        <span>Возраст</span>
        <input type="text" v-model="person_data.age">
      </div>
    </div>

    <div class="fields__field">
      <div class="fields__title">
        <div>Дети (макс. 5)</div>
        <div v-if="this.person_data?.children?.length < 5" @click="addChild" class="field-button">
          <img src="../assets/plus.svg" alt="add">
          <span class="field-button__title">
            Добавить ребенка
          </span>
        </div>
      </div>
      <div class="fields__childs">
        <AppChild v-for="(child, index) in person_data.children" :key="child.id" :index="index" :child="child"
          @deleteChild="deleteChild" @changeChild="changeChild" />
      </div>
    </div>

    <div @click="updatePersonData" class="fields__button">
      Сохранить
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import AppChild from './AppChild.vue'

export default {
  name: 'AppFields',
  components: {
    AppChild
  },
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
  methods: {
    updatePersonData() {
      this.$emit('updatePersonData', this.person_data)
    },
    addChild() {
      if (this.person_data?.children?.length < 5) {
        this.person_data.children.push({
          name: 'Иван',
          age: 10,
          id: Math.random() * 1000
        })
      }
    },
    deleteChild(index) {
      this.person_data.children.splice(index, 1)
      const children_new = this.person_data.children
      Vue.set(this.person_data.children, children_new)
    },
    changeChild(data, index) {
      this.person_data.children[index] = data
      const person_data_new = this.person_data
      this.person_data = JSON.parse(JSON.stringify(person_data_new))
    }
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

.fields {
  display: flex;
  flex-direction: column;

  &__field {
    display: flex;
    flex-direction: column;

    &:not(:last-child) {
      margin-bottom: 44px;
    }
  }

  &__title {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 4px;
    @include montserrat-normal-16;
    color: $colors-second-black;
    margin-bottom: 20px;

    .field-button {
      display: flex;
      align-items: center;
      gap: 4px;
      padding: 10px 20px;
      border-radius: 100px;
      border: 2px solid $colors-primary;

      &:hover {
        @include touchable;
      }

      &__title {
        color: $colors-primary;
        @include montserrat-normal-14;
      }
    }
  }

  &__input {
    position: relative;
    border: 1px solid $colors-gray-l;

    &:not(:last-child) {
      margin-bottom: 10px;
    }

    span {
      position: absolute;
      left: 16px;
      top: 8px;
      @include montserrat-normal-13;
      color: $colors-gray;
    }

    input {
      width: 100%;
      @include montserrat-normal-14;
      padding: 26px 16px 6px;
      outline: none;
      border: 0;
      box-sizing: border-box;
    }
  }

  &__button {
    max-width: 118px;
    margin-top: 30px;
    padding: 10px 0;
    background: $colors-primary;
    border-radius: 100px;
    @include montserrat-normal-14;
    color: $colors-white;
    text-align: center;

    &:hover {
      @include touchable;
    }
  }

  &__childs {
    display: flex;
    flex-direction: column;
    gap: 10px;
  }
}
</style>