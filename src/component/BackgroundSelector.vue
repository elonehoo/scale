<script setup lang="ts">
import Title from './Title.vue'
import Color from 'color'
const props = defineProps<{
  darkColors?:any,
  lightColors?:any,
  lightColorsAmount?:any
}>()
const emits = defineEmits(['setBgColor'])

function getBorderColor(color:string):string{
  return Color(color).luminosity() < 0.5 ? 'hsla(0,0%,100%,0.15)' : 'hsla(0,0%,0%,0.15)'
}
</script>

<template>
  <div>
    <Title>Background</Title>
    <!-- dots wrapper -->
    <div class="h-1/1 flex">
      <!-- dots colum -->
      <div class="DotsColumn">
        <!-- dot -->
        <div class="w-32px h-32px b-rd-1/1 bg-black box-shadow cursor-pointer" @click="emits('setBgColor','black')" :style="{'--borderColor':getBorderColor('black')}"/>
        <div class="w-32px h-32px b-rd-1/1 bg-white box-shadow cursor-pointer" @click="emits('setBgColor','white')" :style="{'--borderColor':getBorderColor('white')}"/>
      </div>
      <!-- dots colum -->
      <div class="DotsColumn">
        <template v-for="(color,index) in props.darkColors" :key="index">
          <div v-if="index < 2" class="w-32px h-32px b-rd-1/1 box-shadow cursor-pointer" :class="`bg-${color}`" @click="emits('setBgColor',`d-${index}`)" :style="{'--borderColor':getBorderColor(color)}"/>
        </template>
      </div>
      <!-- dots colum -->
      <div class="DotsColumn">
        <template v-for="(color,index) in props.lightColors" :key="index">
          <div v-if="index < 2" class="w-32px h-32px b-rd-1/1 box-shadow cursor-pointer" :class="`bg-${color}`" @click="emits('setBgColor',`l-${lightColorsAmount - index}`)" :style="{'--borderColor':getBorderColor(color)}"/>
        </template>
      </div>
    </div>
  </div>

</template>

<style>
.DotsColumn {
  margin-left: 4px;
}

.Dot + .Dot {
  margin-top: 4px;
}
.box-shadow{
  box-shadow: inset 0 0 0.5px 1px var(--borderColor);
}
</style>
