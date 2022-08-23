<template>
  <label class="block font-medium mt-3" :for="name"
    ><slot name="label"></slot>
    <input
      class="ml-3 align-middle"
      type="checkbox"
      :name="name"
      :id="name"
      :checked="modelValue"
      @change="$emit('update:modelValue', $event.target.checked)"
    />
  </label>
</template>

<script>
export default {
  props: {
    modelValue: {
      type: Boolean,
      default: true,
    },
    name: {
      type: String,
      required: true,
    },
  },
  name: 'check-input',
};
</script>
