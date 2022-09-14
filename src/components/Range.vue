<script setup lang="ts">
const props = defineProps<{
  modelValue?:number,
  min?:number,
  max?:number
}>()

defineEmits(['update:modelValue'])
</script>

<template>
  <input type="range" class="range" :min="props.min" :max="props.max" :value="props.modelValue" @input="$emit('update:modelValue', $event.target?.value)">
</template>

<style scoped>
.range{
  --thumbScale: 1;
  width: 96px;
  height: 12px;
  appearance: none;
  margin: 8px 0px;
  display: block;
  cursor: pointer;
  background-color: transparent;
}
</style>
