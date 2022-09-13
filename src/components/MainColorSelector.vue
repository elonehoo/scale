<script setup lang="ts">
import DynamicInput from '~/components/DynamicInput.vue'
import Slider from './Slider.vue';
import { numberToHex } from '~/util/util'

const props = defineProps<{
  mainColor:string,
  r?:number,
  g?:number,
  b?:number
}>()
</script>

<template>
  <!-- input row -->
  <div class="input-row">
    <!-- inputs row item -->
    <div class="inputs-row-item">
      <DynamicInput :color="numberToHex(props.mainColor)" v-model="props.mainColor"  prefix='#' label='Color' />

      <!-- slider wrapper -->
      <div class="flex items-center">
        <div class="mr-12px text-12px leading-16px font-700 relative top-2px">R</div>
        <Slider type='range' min="0" max="255" :value="props.r" />
      </div>

      <!-- slider wrapper -->
      <div class="flex items-center">
        <div class="mr-12px text-12px leading-16px font-700 relative top-2px">G</div>
        <Slider type='range' min="0" max="255" :value="props.g" />
      </div>

      <!-- slider wrapper -->
      <div class="flex items-center">
        <div class="mr-12px text-12px leading-16px font-700 relative top-2px">B</div>
        <Slider type='range' min="0" max="255" :value="props.b" />
      </div>
    </div>
  </div>
</template>

<style scoped>
.input-row{
  display: flex;

  @media (max-width: 720px) {
    flex-direction: column;
  }
}
.inputs-row-item{
  margin-right: 40px;
  flex-shrink: 0;
  width: 192px;
}
</style>
