<template>
  <modal-window v-show="isModalOpen" @close-modal="closeModal">
    <template v-slot:window-title>Добро пожаловать</template>

    <template v-slot:window-description>
      Используя это приложение вы сможете сгенерировать надпись, имитирующую эффект "вырезок из газет".
    </template>

    <template v-slot:button-text>Продолжить</template>
  </modal-window>
  <main class="mx-12 my-8 grid grid-cols-[300px_1fr] gap-8">
    <query-area v-model:query="query" />
    <result-area class="row-span-3" :query="query" :params="settingParams" :key="componentKey" />
    <setting-area @update-setting="handleSettingsUpdate" />
    <button
      class="bg-emerald-400 text-white py-3 rounded-xl w-2/3 justify-self-center hover:bg-emerald-300 transition-colors active:bg-emerald-500"
      @click.prevent="componentKey++"
    >
      Сгенерировать
    </button>
  </main>
</template>

<script>
import QueryArea from '@/components/QueryArea';
import ResultArea from '@/components/ResultArea';
import SettingArea from '@/components/SettingArea';

export default {
  components: { QueryArea, ResultArea, SettingArea },
  name: 'App',
  data() {
    return {
      isModalOpen: false,
      query: '',
      settingParams: null,
      componentKey: 0,
    };
  },
  methods: {
    closeModal() {
      this.isModalOpen = false;
    },
    handleSettingsUpdate(params) {
      this.settingParams = params;
    },
  },
};
</script>

<style lang="scss"></style>
