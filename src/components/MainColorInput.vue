<script setup lang="ts">
const props = defineProps<{
  modelValue:string
}>()

defineEmits(['update:modelValue'])
</script>

<template>
  <div class="relative w-auto h-1/1">
    <input
     class="main-color-input"
     :value="props.modelValue"
     @input="$emit('update:modelValue', $event.target?.value)"
    />
    <div class="main-color-input-text">{{props.modelValue}}</div>
  </div>
  <div class="relative w-auto h-1/1">
    <input type="text" class="other-input" readonly tabindex="-1" value/>
    <div class="other-input-text"></div>
  </div>
</template>

<style scoped>
.main-color-input{
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
.main-color-input-text{
  font-size: 40px;
  font-weight: inherit;
  line-height: 1;
  opacity: 0;
  transform: translateY(236px) scale(0);
}
.other-input{
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
.other-input-text {
  font-size: 40px;
  font-weight: inherit;
  line-height: 1;
  opacity: 0;
  transform: translateY(236px) scale(0);
}
</style>
