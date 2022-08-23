<template>
  <div class="p-5 rounded-md shadow-md bg-white">
    <h2 class="pb-4 mb-3 border-b border-b-gray-200">Настройки</h2>
    <form>
      <range-input :name="'font-size'" v-model.number="params.fontSize">
        <template #label>Размер шрифта:</template>

        <template #leftParam>
          <span class="text-sm">A</span>
        </template>

        <template #rightParam>
          <span class="text-xl">A</span>
        </template>
      </range-input>

      <range-input :name="'rotate-angle'" v-model.number="params.rotateAngle" :max="12">
        <template #label>Максимальный угол поворота:</template>

        <template #leftParam>
          <span class="text-md self-start">0&deg;</span>
        </template>

        <template #rightParam>
          <span class="text-md">360&deg;</span>
        </template>
      </range-input>

      <range-input :name="'bg-width'" v-model.number="params.bgWidth">
        <template #label>Ширина фона:</template>

        <template #leftParam>
          <span class="text-md self-start">&#9646;</span>
        </template>

        <template #rightParam>
          <span class="text-md">&#9632;</span>
        </template>
      </range-input>

      <range-input :name="'bg-height'" v-model.number="params.bgHeight">
        <template #label>Высота фона:</template>

        <template #leftParam>
          <span class="text-md self-start">&#9632;</span>
        </template>

        <template #rightParam>
          <span class="text-md">&#9644;</span>
        </template>
      </range-input>

      <range-input :name="'margins'" v-model.number="params.margins">
        <template #label>Отступы между буквами:</template>

        <template #leftParam>
          <span class="text-md tracking-normal">AB</span>
        </template>

        <template #rightParam>
          <span class="text-md tracking-[.5em]">AB</span>
        </template>
      </range-input>

      <check-input :checked="true" :name="'bg-texture'" v-model="params.isTextured">
        <template #label>Текстуры для фона:</template>
      </check-input>
    </form>
  </div>
</template>

<script>
export default {
  name: 'setting-area',
  data() {
    return {
      params: {
        fontSize: 6,
        rotateAngle: 1,
        bgWidth: 6,
        bgHeight: 6,
        margins: 6,
        isTextured: true,
      },
    };
  },
  watch: {
    params: {
      handler() {
        this.$emit('updateSetting', this.params);
      },
      deep: true,
    },
  },
  mounted() {
    this.$emit('updateSetting', this.params);
  },
};
</script>
