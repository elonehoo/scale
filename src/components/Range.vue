<script setup lang="ts">
const props = defineProps<{
  modelValue?:any,
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
.range:focus {
  outline: none;
  --thumbScale: 1.2;
}
.range::-webkit-slider-runnable-track {
  width: 100%;
  height: 2px;
  cursor: pointer;
  background: var(--bodyDimmed);
  border-radius: 2px;
}
.range::-webkit-slider-thumb {
  height: 10px;
  width: 10px;
  transform: scale(var(--thumbScale));
  border-radius: 50%;
  color: inherit;
  background: var(--bodyColor);
  cursor: pointer;
  appearance: none;
  margin-top: -4px;
}
.range::-moz-range-track {
  width: 100%;
  height: 2px;
  cursor: pointer;
  background: var(--bodyDimmed);
  border-radius: 2px;
}
.range::-moz-range-thumb {
  height: 10px;
  width: 10px;
  transform: scale(var(--thumbScale));
  border-radius: 50%;
  color: inherit;
  background: var(--bodyColor);
  cursor: pointer;
  appearance: none;
  margin-top: -4px;
}
.range::-ms-track {
  width: 100%;
  height: 2px;
  cursor: pointer;
  background: var(--bodyDimmed);
  border-radius: 2px;
}
.range::-ms-fill-lower {
  background: #D8D8D8;
  border-radius: 2px;
}
.range::-ms-fill-upper {
  background: #D8D8D8;
  border-radius: 2px;
}
.range::-ms-thumb {
height: 10px;
width: 10px;
transform: scale(var(--thumbScale));
border-radius: 50%;
color: inherit;
background: var(--bodyColor);
cursor: pointer;
appearance: none;
margin-top: -4px;
}
.range:focus::-ms-fill-lower {
  background: #D8D8D8;
}
.range:focus::-ms-fill-upper {
  background: #D8D8D8;
}
</style>
