<template>
  <div class="header-wrapper">
    <div class="header block">
      <img src="../assets/logo.svg" alt="logo">
      <div class="header__content">
        <div @click="$emit('setPage', 'fields')" class="header__button">Форма</div>
        <div @click="$emit('setPage', 'preview')" class="header__button">Превью</div>
      </div>
      <div></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AppHeader',
}
</script>

<style scoped lang="scss">
@import "@/assets/scss/main.scss";

.header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 24px 0;

  &-wrapper {
    margin-bottom: 30px;
    box-shadow: 0px 1px 0px 0px rgba(17, 17, 17, 0.10);
  }

  &__content {
    display: flex;
    gap: 24px;
  }

  &__button {
    @include montserrat-normal-14;
    color: $colors-gray;

    &:hover {
      @include touchable;
    }
  }
}
</style>