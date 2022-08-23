<template>
  <label class="font-medium" :for="name"><slot name="label"></slot></label><br />
  <div class="mt-2 flex items-center justify-between">
    <slot name="leftParam"></slot>
    <input
      class="basis-3/5"
      type="range"
      :name="name"
      :id="name"
      :min="min"
      :max="max"
      step="1"
      :value="modelValue"
      @input="$emit('update:modelValue', $event.target.value)"
    />
    <slot name="rightParam"></slot>
  </div>
</template>

<script>
export default {
  inheritAttrs: false,
  name: 'range-input',
  props: {
    name: {
      type: String,
      required: true,
    },
    modelValue: {
      type: Number,
      default: 6,
    },
    min: {
      type: Number,
      default: 1,
    },
    max: {
      type: Number,
      default: 11,
    },
  },
};
</script>
