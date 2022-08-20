<template>
  <modal-window v-if="isModalOpen" @close-modal="closeModal">
    <template v-slot:window-title>Добро пожаловать</template>

    <template v-slot:window-description>
      Используя это приложение вы сможете сгенерировать надпись, имитирующую
      эффект "вырезок из газет".
    </template>

    <template v-slot:button-text>Продолжить</template>
  </modal-window>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      isModalOpen: true,
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
