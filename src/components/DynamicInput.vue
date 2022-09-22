<script setup lang="ts">
const props = defineProps<{
  value:number
}>()

const emits = defineEmits(['update:value'])
</script>

<template>
  <div class="flex mb-16px">
    <div class="relative w-1/1 h-1/1">
      <input class="dynamic-input" type="number" min="0" v-model="props.value" @input="emits('update:value',$event.target?.value)" />
      <div class="dynamic-input-text">{{props.value}}</div>
    </div>
    <div class="relative w-auto h-1/1">
      <input class="dynamic-input-shadow" type="text" readonly tabindex="-1">
      <div class="dynamic-input-shadow-text" />
    </div>
  </div>
</template>

<style scoped>
.dynamic-input{
  color: inherit;
  font-size: 40px;
  font-family: inherit;
  font-weight: inherit;
  line-height: 1;
  padding: 0px;
  border: 0px;
  width: 100%;
  position: absolute;
  top: 0px;
  height: 100%;
  background-color: transparent;
  appearance: textfield;
  margin: 0px;
}
.dynamic-input-text{
  font-size: 40px;
  font-weight: inherit;
  line-height: 1;
  opacity: 0;
  transform: translateY(236px) scale(0);
}
.dynamic-input-shadow{
  color: inherit;
  font-size: 40px;
  font-family: inherit;
  font-weight: inherit;
  line-height: 1;
  padding: 0px;
  border: 0px;
  width: 100%;
  position: absolute;
  top: 0px;
  height: 100%;
  background-color: transparent;
  appearance: textfield;
  margin: 0px;
  user-select: none;
  opacity: 0.4;
}
.dynamic-input-shadow-text{
  font-size: 40px;
  font-weight: inherit;
  line-height: 1;
  opacity: 0;
  transform: translateY(236px) scale(0);
}
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
}
input[type="number"]{
  -moz-appearance: textfield;
}
</style>
