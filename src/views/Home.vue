<template>
  <div class="container mx-auto flex flex-wrap justify-center gap-3 pt-10">
    <div v-for="(k, i) in surahList" :key="i">
      <router-link
        :to="`/surah/${i + 1}`"
        class="
          h-40
          w-44
          card
          p-5
          dark:glass dark:text-white
          shadow
          bg-gradient-to-tr
          hover:from-indigo-300
          from-indigo-200
          to-blue-200
          transform
          hover:scale-105
          transition
          duration-300
        "
      >
        <div>
          <button class="btn btn-circle bg-indigo-500">{{ i + 1 }}</button>
        </div>
        <div class="mt-4">
          <h2 class="font-bold text-2xl">{{ k.title }}</h2>
          <h3>{{ k.place }}</h3>
        </div>
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      surahList: [],
    };
  },
  methods: {
    async getSurahList() {
      const res = await fetch(
        "https://raw.githubusercontent.com/semarketir/quranjson/master/source/surah.json"
      );
      const data = await res.json();
      this.surahList = data;
    },
  },
  created() {
    this.getSurahList();
  },
};
</script>

<style lang="scss" scoped>
</style>