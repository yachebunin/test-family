<template>
  <div class="footer">
    all rights reserved
  </div>
</template>

<script>
export default {
  name: 'AppFooter',
}
</script>

<style scoped lang="scss">
@import "@/assets/scss/main.scss";

.footer {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: auto;
  padding: 30px 0;
  background: $colors-gray-m;
  color: $colors-black;
}
</style>