<template>
  <textarea
    :value="query"
    @input="makeQuary"
    name="query-area"
    cols="30"
    rows="10"
    placeholder="Введите текст здесь..."
    class="outline-none border-none p-5 rounded-md resize-none shadow-md"
  ></textarea>
</template>

<script>
export default {
  name: 'query-area',
  props: {
    query: String,
  },
  emits: {
    'update:query': null,
  },
  data() {
    return {};
  },
  methods: {
    makeQuary(event) {
      this.$emit('update:query', event.target.value);
    },
  },
};
</script>

<style lang="scss" scoped></style>
