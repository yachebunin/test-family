<template>
  <div class="child">
    <div class="child__input">
      <span>Имя</span>
      <input type="text" v-model="child_data.name" @change="$emit('changeChild', child_data, index)">
    </div>
    <div class="child__input">
      <span>Возраст</span>
      <input type="text" v-model="child_data.age" @change="$emit('changeChild', child_data, index)">
    </div>
    <div class="child__delete" @click="$emit('deleteChild', index)">
      Удалить
    </div>
  </div>
</template>

<script>
export default {
  name: 'AppChild',
  data() {
    return {
      child_data: {
        type: Object,
        default: () => { }
      }
    }
  },
  props: {
    child: {
      type: Object,
      default: () => { }
    },
    index: {
      type: Number,
      default: 0
    }
  },
  mounted() {
    this.child_data = JSON.parse(JSON.stringify(this.child))
  },
  watch: {
    child() {
      this.child_data = this.child
    }
  }
}
</script>

<style scoped lang="scss">
@import "@/assets/scss/main.scss";

.child {
  display: flex;
  align-items: center;
  gap: 18px;

  &__input {
    position: relative;
    flex-grow: 1;
    border: 1px solid $colors-gray-l;

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

  &__delete {
    @include montserrat-normal-14;
    color: $colors-primary;

    &:hover {
      @include touchable;
    }
  }
}
</style>