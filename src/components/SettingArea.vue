<template>
  <div class="p-5 rounded-md shadow-md bg-white">
    <h2 class="pb-4 border-b border-b-gray-200">Настройки</h2>
    <form>
      <div class="mt-3">
        <label class="font-medium" for="font-size">Размер шрифта:</label><br />
        <div class="mt-2 flex items-center justify-between">
          <span class="text-sm">A</span>
          <input class="basis-3/5" type="range" name="font-size" id="font-size" min="1" max="10" step="1" />
          <span class="text-xl">A</span>
        </div>
      </div>
      <div class="mt-3">
        <label class="font-medium" for="rotate-angle">Максимальный угол поворота:</label><br />
        <div class="mt-2 flex justify-between">
          <span class="text-md self-start">0&deg;</span>
          <input class="basis-3/5" type="range" name="rotate-angle" id="rotate-angle" min="1" max="10" step="1" />
          <span class="text-md">360&deg;</span>
        </div>
      </div>
      <div class="mt-3">
        <label class="font-medium" for="bg-width">Ширина "вырезок":</label><br />
        <div class="mt-2 flex justify-between">
          <span class="text-md self-start">&#9646;</span>
          <input class="basis-3/5" type="range" name="bg-width" id="bg-width" min="1" max="10" step="1" />
          <span class="text-md">&#9632;</span>
        </div>
      </div>
      <div class="mt-3">
        <label class="font-medium" for="bg-height">Высота "вырезок":</label><br />
        <div class="mt-2 flex justify-between">
          <span class="text-md self-start">&#9632;</span>
          <input class="basis-3/5" type="range" name="bg-height" id="bg-height" min="1" max="10" step="1" />
          <span class="text-md">&#9644;</span>
        </div>
      </div>
      <div class="mt-3">
        <label class="font-medium" for="margins">Отступы между буквами:</label><br />
        <div class="mt-2 flex items-center justify-between">
          <span class="text-md tracking-normal">AB</span>
          <input class="basis-3/5" type="range" name="margins" id="margins" min="1" max="10" step="1" />
          <span class="text-md tracking-[.5em]">AB</span>
        </div>
      </div>
      <div class="mt-3">
        <label class="font-medium" for="bg-texture">Текстуры для фона:</label>
        <input class="ml-3 align-middle" type="checkbox" name="bg-texture" id="bg-texture" value="isTextured" checked />
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: 'setting-area',
};
</script>

<style lang="scss" scoped></style>
