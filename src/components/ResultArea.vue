<template>
  <div class="flex justify-center items-center self-stretch text-3xl">
    <span
      class="whitespace-pre-wrap"
      :style="{ 'font-family': letter.font }"
      v-for="(letter, idx) of calculatedQuery"
      :key="idx"
      >{{ letter.letter }}</span
    >
  </div>
</template>

<script>
const FONTS = [
  'Alegreya',
  'Alumni Sans Collegiate One',
  'Amatic SC',
  'Bellota Text',
  'Brygada 1918',
  'Caveat',
  'Comfortaa',
  'Comforter Brush',
  'Cormorant Garamond',
  'Cormorant Infant',
  'Exo 2',
  'IBM Plex Serif',
  'Lobster',
  'Merriweather',
  'Neucha',
  'Noto Serif Display',
  'Oi',
  'Orelega One',
  'Pacifico',
  'Pattaya',
  'Playfair Display',
  'Playfair Display SC',
  'Prata',
  'Press Start 2P',
  'Roboto',
  'Rubik Mono One',
  'Ruslan Display',
  'Russo One',
  'Yanone Kaffeesatz',
  'Yeseva One',
];

export default {
  name: 'result-area',
  props: {
    query: String,
  },
  data() {
    return {
      newQuery: [],
      // font: '',
    };
  },
  watch: {
    query() {
      // ЗДЕСЬ ПРОИСХОДИТ ЛОГИКА ОБРАБОТКИ ТЕКСТА
      // this.newQuery = this.query.split('').map(l => {
      //   let random = Math.ceil(Math.random() * 10);
      //   let font = `'${FONTS[random]}', serif`;
      //   return { letter: l, font: font };
      // });
    },
  },
  computed: {
    calculatedQuery() {
      return this.query.split('').map(l => {
        let random = Math.ceil(Math.random() * 10);
        let font = `'${FONTS[random]}', serif`;
        return { letter: l, font: font };
      });
    },
  },
};
</script>

<style lang="scss" scoped></style>
