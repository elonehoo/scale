<script setup lang="ts">
const props = defineProps<{
  color?:string
}>()

const emit = defineEmits(['update-bg'])
</script>

<template>
  <div @click="emit('update-bg',props.color)" class="raw" :style="{'background':`${props.color}`}" />
</template>

<style scoped>
.raw{
  width: 32px;
  height: 32px;
  border-radius: 100%;
  box-shadow: inset 0 0 0.5px 1px var(--borderColor);
  cursor: pointer;
}
</style>
