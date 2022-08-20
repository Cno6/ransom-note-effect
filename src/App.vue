<template>
  <modal-window v-show="isModalOpen" @close-modal="closeModal">
    <template v-slot:window-title>Добро пожаловать</template>

    <template v-slot:window-description>
      Используя это приложение вы сможете сгенерировать надпись, имитирующую
      эффект "вырезок из газет".
    </template>

    <template v-slot:button-text>Продолжить</template>
  </modal-window>
  <main class="mx-12 my-8 grid grid-cols-[300px_1fr] gap-8">
    <query-area v-model:query="query" />
    <result-area class="row-span-2" :query="query" />
    <setting-area />
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
    };
  },
  methods: {
    closeModal() {
      this.isModalOpen = false;
    },
  },
};
</script>

<style lang="scss"></style>
