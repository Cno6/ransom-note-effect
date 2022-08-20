<template>
  <div
    class="h-screen bg-black bg-opacity-50 flex justify-center items-center p-5"
  >
    <div
      class="flex flex-col justify-center items-center bg-gray-100 p-5 rounded-md text-center"
    >
      <h1 class="mb-4 font-bold text-2xl">
        <slot name="window-title"></slot>
      </h1>
      <p class="max-w-md mb-5">
        <slot name="window-description"></slot>
      </p>
      <button
        @click="handleModalButton"
        type="button"
        class="px-3 py-1.5 rounded-md bg-green-500 text-white hover:bg-emerald-400 active:bg-cyan-500 transition-colors"
      >
        <slot name="button-text"></slot>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'modal-window',
  data() {
    return {};
  },
  methods: {
    handleModalButton() {
      this.$emit('closeModal');
    },
  },
};
</script>

<style lang="scss" scoped></style>
