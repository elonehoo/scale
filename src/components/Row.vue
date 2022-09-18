<script setup lang="ts">
const props = defineProps<{
  color:string,
  main?:boolean
}>()
</script>

<template>
  <div class="row" :class="props.main ? 'row-192px' : 'row-72px'" :style="{'background':props.color}"/>
</template>

<style scoped>
.row{
  position: relative;
  height: 72px;
  width: 100%;
  flex-shrink: 1;
  cursor: pointer;
}
.row-72px{
  max-width: 72px;
}
.row-192px{
  max-width: 192px;
  min-width: 192px;
}
</style>
