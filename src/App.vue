<template>
  <div
    class="
      min-h-screen
      pb-10
      bg-gradient-to-t
      from-blue-50
      to-indigo-50
      dark:from-gray-700 dark:to-gray-900
      bangla
    "
  >
    <Header />
    <router-view></router-view>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
export default {
  setup() {
    return {};
  },
  components: { Header },
};
</script>

<style lang="scss" scoped>
</style>