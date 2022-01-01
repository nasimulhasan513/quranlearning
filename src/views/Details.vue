<template>
  <div class="container mx-auto mt-10 space-y-5" v-if="surah">
    <div
      class="
        dark:glass
        shadow
        bg-gradient-to-tr
        from-blue-100
        to-indigo-100
        card
        p-4
        space-y-3
        text-center
      "
      v-for="(s, i) in surah.verse"
      :key="i"
    >
      <p class="amiri text-2xl dark:text-gray-100">{{ s }}</p>
      <p class="sora dark:text-gray-50" v-if="translation">
        {{ translation.verse[i] }}
      </p>
      <audio controls class="mx-auto">
        <source
          :src="`https://rawgit.com/semarketir/quranjson/master/source/audio/${
            surah.index
          }/${formetNumber(i)}.mp3`"
          type="audio/mp3"
        />
        Your browser does not support the audio element.
      </audio>
    </div>
  </div>
  <div class="text-center" v-else>
    <button class="btn btn-circle loading"></button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      surah: null,
      translation: null,
    };
  },
  methods: {
    async getSurah() {
      const res = await fetch(
        `https://raw.githubusercontent.com/semarketir/quranjson/master/source/surah/surah_${this.$route.params.id}.json`
      );
      const data = await res.json();
      this.surah = data;
      console.log(data);
    },
    async getTranslation() {
      const res = await fetch(
        `https://raw.githubusercontent.com/semarketir/quranjson/master/source/translation/en/en_translation_${this.$route.params.id}.json`
      );
      const data = await res.json();
      this.translation = data;
    },
    formetNumber(i) {
      let n = parseInt(i.split("_")[1]);

      if (n < 10) return `00${n}`;
      if (n > 9 && n < 100) {
        return `0${n}`;
      }
      if (n > 100) return `${n}`;
    },
  },
  created() {
    this.getSurah();
    this.getTranslation();
  },
};
</script>

<style lang="scss" scoped>
</style>