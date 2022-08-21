<template>
  <div class="flex flex-wrap justify-center items-center self-stretch">
    <span
      v-for="(letter, idx) of calculatedResult"
      :key="idx"
      ref="letter"
      :style="{
        'font-family': letter.font,
        'padding-right': letter.paddingX,
        'padding-top': letter.paddingY,
        'padding-left': letter.paddingX,
        'padding-bottom': letter.paddingY,
        'margin-right': letter.marginRight,
        'font-size': letter.letterSize,
        color: letter.letterColor,
        'text-shadow': letter.shadow,
        'background-color': letter.bgColor,
        visibility: letter.visibility,
        'text-stroke': letter.textStroke,
        transform: letter.transformRotate,
      }"
      class="whitespace-pre-wrap leading-none shadow-md mr-5 overflow-hidden"
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

/* 
TODO: 
  [x] Сделать visibility: hidden, если символ = пробел
  2. Делать новую строку по нажатию Enter в Input
  [x] Сделать добавление случайных margin
  [x] Переделать случайные padding с right-top на все значения.
  [x] Добавить генерацию случайного фона (цвет).
  [x] Добавить border в 10% случаев. 
  [x] Добавить случайный поворот.
  8. Добавить случайную текстуру фона.
*/

export default {
  name: 'result-area',
  props: {
    query: String,
  },
  data() {
    return {
      maxPaddingX: 60,
      minPaddingX: 10,
      maxPaddingY: 40,
      minPaddingY: 10,
      maxletterSize: 96,
      minletterSize: 48,
    };
  },
  watch: {},
  computed: {
    calculatedResult() {
      return this.query.split('').map(l => {
        // FONT-FAMILY
        const randomFontIndex = Math.floor(Math.random() * FONTS.length);
        const fontFamilyCssValue = `'${FONTS[randomFontIndex]}', serif`;

        // PADDINGS
        let randomPaddingValue = Math.round(Math.random() * (this.maxPaddingX - this.minPaddingX) + this.minPaddingX);
        const paddingX = `${randomPaddingValue / 2}px`;
        randomPaddingValue = Math.round(Math.random() * (this.maxPaddingY - this.minPaddingY) + this.minPaddingY);
        const paddingY = `${randomPaddingValue / 2}px`;

        // MARGINS
        const randomMarginValue = Math.round(Math.random() * (60 - 20) + 20);
        const margin = `${randomMarginValue / 2}px`;

        // LETTER SIZE
        const randomletterSize = Math.round(
          Math.random() * (this.maxletterSize - this.minletterSize) + this.minletterSize
        );
        const letterSize = `${randomletterSize}px`;

        // LETTER COLOR
        const COLORS = [
          'gainsboro',
          'black',
          'red',
          'green',
          'cyan',
          'aqua',
          'blue',
          'yellow',
          'purple',
          'peru',
          'violet',
          'orange',
          'pink',
        ];
        const randomColorIndex = Math.floor(Math.random() * COLORS.length);
        const letterColor = `${COLORS[randomColorIndex]}`;

        // LETTER SHADOW
        const hasShadow = Math.random();
        let letterShadow = '';
        if (hasShadow < 0.3) {
          const shadowXOffset = Math.round(Math.random() * (15 - 0) + 0);
          const shadowYOffset = Math.round(Math.random() * (5 - 0) + 0);
          let randomShadowColorIndex = Math.floor(Math.random() * COLORS.length);
          if (randomShadowColorIndex === randomColorIndex) {
            randomShadowColorIndex++;
          }
          letterShadow = `${shadowXOffset}px ${shadowYOffset}px ${COLORS[randomShadowColorIndex]}`;
        }

        // BACKGROUND COLOR
        let randomBgColorIndex = Math.floor(Math.random() * COLORS.length);
        if (randomBgColorIndex === randomColorIndex) {
          randomBgColorIndex--;
        }
        const bgColor = `${COLORS[randomBgColorIndex]}`;

        let visibility = 'visible';
        if (l === ' ') {
          visibility = 'hidden';
        }

        // TEXT STROKE
        const hasStroke = Math.random();
        let textStroke = '';
        if (hasStroke < 0.1) {
          textStroke = `2px black`;
        }

        // ROTATE
        const hasRotate = Math.random();
        let rotate = `rotate(0deg)`;
        if (hasRotate < 0.3) {
          const randomRotateDegree = Math.random() * (35 + 35) - 35;
          rotate = `rotate(${randomRotateDegree}deg)`;
        } else {
          const randomRotateDegree = Math.random() * (4 + 4) - 4;
          rotate = `rotate(${randomRotateDegree}deg)`;
        }

        return {
          letter: l,
          font: fontFamilyCssValue,
          paddingX: paddingX,
          paddingY: paddingY,
          marginRight: margin,
          letterSize: letterSize,
          letterColor: letterColor,
          shadow: letterShadow,
          bgColor: bgColor,
          visibility: visibility,
          textStroke: textStroke,
          transformRotate: rotate,
        };
      });
    },
  },
};
</script>

<style lang="scss" scoped></style>
