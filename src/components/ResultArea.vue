<template>
  <div class="flex flex-wrap justify-center items-center self-stretch" ref="div">
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
        'clip-path': letter.corners,
        'background-image': letter.bgTexture,
        'background-repeat': 'no-repeat',
        'background-size': '150% 150%',
        'background-position': 'center',
        'background-blend-mode': letter.blendMode,
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
  [x] Добавить случайную текстуру фона.
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
        if (l === ' ' || l === '\n') {
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
          const randomRotateDegree = Math.random() * (25 + 25) - 25;
          rotate = `rotate(${randomRotateDegree}deg)`;
        } else {
          const randomRotateDegree = Math.random() * (4 + 4) - 4;
          rotate = `rotate(${randomRotateDegree}deg)`;
        }

        // CORNERS
        const corners = [[], [], [], []];
        const cornerMax = 10;

        corners.forEach((corn, index) => {
          switch (index) {
            case 0:
              if (Math.random() > 0.5) {
                corn.push(Math.random() * cornerMax, Math.random() * cornerMax);
              } else {
                corn.push(0, 0);
              }
              break;
            case 1:
              if (Math.random() > 0.5) {
                corn.push(Math.random() * (100 - (100 - cornerMax)) + (100 - cornerMax), Math.random() * cornerMax);
              } else {
                corn.push(100, 0);
              }
              break;
            case 2:
              if (Math.random() > 0.5) {
                corn.push(
                  Math.random() * (100 - (100 - cornerMax)) + (100 - cornerMax),
                  Math.random() * (100 - (100 - cornerMax)) + (100 - cornerMax)
                );
              } else {
                corn.push(100, 100);
              }
              break;
            case 3:
              if (Math.random() > 0.5) {
                corn.push(Math.random() * cornerMax, Math.random() * (100 - (100 - cornerMax)) + (100 - cornerMax));
              } else {
                corn.push(0, 100);
              }
              break;
          }
        });

        const cornersTemplate = `polygon(${corners[0][0]}% ${corners[0][1]}%, ${corners[1][0]}% ${corners[1][1]}%, ${corners[2][0]}% ${corners[2][1]}%, ${corners[3][0]}% ${corners[3][1]}%)`;

        // BACKGROUND TEXTURES
        let bgTexture;
        let blendMode = 'multiply';
        if (Math.random() > 0.8) {
          let numImage = Math.floor(Math.random() * (9 - 1) + 1);
          bgTexture = `url(${require('@/assets/textures/texture-' + numImage + '.png')})`;
          if (numImage == 4) {
            blendMode = 'soft-light';
          }
        } else {
          bgTexture = false;
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
          corners: cornersTemplate,
          bgTexture: bgTexture,
          blendMode: blendMode,
        };
      });
    },
  },
};
</script>

<style lang="scss" scoped></style>
