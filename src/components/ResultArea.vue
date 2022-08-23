<template>
  <div class="flex flex-wrap justify-center items-center self-stretch">
    <span
      v-for="(letter, idx) of calculatedResult"
      :key="idx"
      ref="letter"
      :style="{
        'font-family': letter.font,
        padding: letter.padding,
        'margin-right': letter.marginRight,
        'font-size': letter.fontSize,
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
        'font-weight': letter.fontWeight,
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
const COLORS = [
  'AliceBlue',
  'AntiqueWhite',
  'Aqua',
  'Aquamarine',
  'Azure',
  'Beige',
  'Bisque',
  'Black',
  'BlanchedAlmond',
  'Blue',
  'BlueViolet',
  'Brown',
  'BurlyWood',
  'CadetBlue',
  'Chartreuse',
  'Chocolate',
  'Coral',
  'CornflowerBlue',
  'Cornsilk',
  'Crimson',
  'Cyan',
  'DarkBlue',
  'DarkCyan',
  'DarkGoldenrod',
  'DarkGray',
  'DarkGreen',
  'DarkGrey',
  'DarkKhaki',
  'DarkMagenta',
  'DarkOliveGreen',
  'DarkOrange',
  'DarkOrchid',
  'DarkRed',
  'DarkSalmon',
  'DarkSeaGreen',
  'DarkSlateBlue',
  'DarkSlateGray',
  'DarkSlateGrey',
  'DarkTurquoise',
  'DarkViolet',
  'DeepPink',
  'DeepSkyBlue',
  'DimGray',
  'DodgerBlue',
  'FireBrick',
  'FloralWhite',
  'ForestGreen',
  'Fuchsia',
  'Gainsboro',
  'GhostWhite',
  'Gold',
  'Goldenrod',
  'Gray',
  'Green',
  'GreenYellow',
  'Grey',
  'Honeydew',
  'HotPink',
  'IndianRed',
  'Indigo',
  'Ivory',
  'Khaki',
  'Lavender',
  'LavenderBlush',
  'LawnGreen',
  'LemonChiffon',
  'LightBlue',
  'LightCoral',
  'LightCyan',
  'LightGoldenrodYellow',
  'LightGray',
  'LightGreen',
  'LightGrey',
  'LightPink',
  'LightSalmon',
  'LightSeaGreen',
  'LightSkyBlue',
  'LightSlateGray',
  'LightSlateGrey',
  'LightSteelBlue',
  'LightYellow',
  'Lime',
  'LimeGreen',
  'Linen',
  'Magenta',
  'Maroon',
  'MediumAquamarine',
  'MediumBlue',
  'MediumOrchid',
  'MediumPurple',
  'MediumSeaGreen',
  'MediumSlateBlue',
  'MediumSpringGreen',
  'MediumTurquoise',
  'MediumVioletRed',
  'MidnightBlue',
  'MintCream',
  'MistyRose',
  'Moccasin',
  'NavajoWhite',
  'Navy',
  'OldLace',
  'Olive',
  'OliveDrab',
  'Orange',
  'OrangeRed',
  'Orchid',
  'PaleGoldenrod',
  'PaleGreen',
  'PaleTurquoise',
  'PaleVioletRed',
  'PapayaWhip',
  'PeachPuff',
  'Peru',
  'Pink',
  'Plum',
  'PowderBlue',
  'Purple',
  'Rebeccapurple',
  'Red',
  'RosyBrown',
  'RoyalBlue',
  'SaddleBrown',
  'Salmon',
  'SandyBrown',
  'SeaGreen',
  'Seashell',
  'Sienna',
  'Silver',
  'SkyBlue',
  'SlateBlue',
  'SlateGray',
  'SlateGrey',
  'Snow',
  'SpringGreen',
  'SteelBlue',
  'Tan',
  'Teal',
  'Thistle',
  'Tomato',
  'Turquoise',
  'Violet',
  'Wheat',
  'White',
  'WhiteSmoke',
  'Yellow',
  'YellowGreen',
];

export default {
  name: 'result-area',
  props: {
    query: String,
    params: Object,
  },
  data() {
    return {};
  },
  methods: {
    calculatePaddings() {
      const maxPaddingX = 10 * this.params.bgWidth;
      const minPaddingX = 5 * this.params.bgWidth;
      const maxPaddingY = 10 * this.params.bgHeight;
      const minPaddingY = 5 * this.params.bgHeight;
      const paddingX = `${Math.round(Math.random() * (maxPaddingX - minPaddingX) + minPaddingX) / 2}px`;
      const paddingY = `${Math.round(Math.random() * (maxPaddingY - minPaddingY) + minPaddingY) / 2}px`;
      return `${paddingY} ${paddingX} ${paddingY} ${paddingX}`;
    },
    calculateLetterSize() {
      const maxletterSize = 25 * this.params.fontSize;
      const minletterSize = 18 * this.params.fontSize;
      const randomletterSize = Math.round(Math.random() * (maxletterSize - minletterSize) + minletterSize);
      return `${randomletterSize}px`;
    },
    calculateFont() {
      const randomFontIndex = Math.floor(Math.random() * FONTS.length);
      return `'${FONTS[randomFontIndex]}', serif`;
    },
    calculateMargins() {
      const maxMargins = 10 * this.params.margins;
      const minMargins = 3 * this.params.margins;
      const randomMarginValue = Math.round(Math.random() * (maxMargins - minMargins) + minMargins);
      return `${randomMarginValue / 2}px`;
    },
    calculateColor() {
      const randomColorIndex = Math.floor(Math.random() * COLORS.length);
      return `${COLORS[randomColorIndex]}`;
    },
    calculateShadow() {
      const hasShadow = Math.random();
      if (hasShadow < 0.3) {
        const shadowXOffset = Math.round(Math.random() * (15 - 0) + 0);
        const shadowYOffset = Math.round(Math.random() * (5 - 0) + 0);
        let randomShadowColorIndex = Math.floor(Math.random() * COLORS.length);
        return `${shadowXOffset}px ${shadowYOffset}px ${COLORS[randomShadowColorIndex]}`;
      }
    },
    calculateBgColor() {
      let randomBgColorIndex = Math.floor(Math.random() * COLORS.length);
      return `${COLORS[randomBgColorIndex]}`;
    },
    calculateTextStroke() {
      const hasStroke = Math.random();
      if (hasStroke < 0.1) {
        return `2px black`;
      }
      return '';
    },
    calculateRotate() {
      const hasRotate = Math.random();
      const maxRotateAngle = 30 * this.params.rotateAngle;
      const minRotateAngle = 4 * this.params.rotateAngle;
      if (hasRotate < 0.3) {
        const randomRotateDegree = Math.random() * (maxRotateAngle + maxRotateAngle) - maxRotateAngle;
        return `rotate(${randomRotateDegree}deg)`;
      } else {
        const randomRotateDegree = Math.random() * (minRotateAngle + minRotateAngle) - minRotateAngle;
        return `rotate(${randomRotateDegree}deg)`;
      }
    },
    calculateCorners() {
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
      return `polygon(${corners[0][0]}% ${corners[0][1]}%, ${corners[1][0]}% ${corners[1][1]}%, ${corners[2][0]}% ${corners[2][1]}%, ${corners[3][0]}% ${corners[3][1]}%)`;
    },
    calculateFontWeight() {
      return Math.round(Math.random() * (9 - 1) + 1) * 100;
    },
  },
  computed: {
    calculatedResult() {
      return this.query.split('').map(l => {
        // VISIBILITY FOR SPACES AND NEW LINES
        let visibility = 'visible';
        if (l === ' ' || l === '\n') {
          visibility = 'hidden';
        }

        // BACKGROUND TEXTURES
        let bgTexture;
        let blendMode = 'multiply';
        if (Math.random() > 0.8 && this.params.isTextured) {
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
          font: this.calculateFont(),
          padding: this.calculatePaddings(),
          marginRight: this.calculateMargins(),
          letterColor: this.calculateColor(),
          shadow: this.calculateShadow(),
          bgColor: this.calculateBgColor(),
          visibility: visibility,
          textStroke: this.calculateTextStroke(),
          transformRotate: this.calculateRotate(),
          corners: this.calculateCorners(),
          bgTexture: bgTexture,
          blendMode: blendMode,
          fontWeight: this.calculateFontWeight(),
          fontSize: this.calculateLetterSize(),
        };
      });
    },
  },
};
</script>
