<script setup lang="ts">
import ColorBlock from './ColorBlock.vue'
import { isValidHex, numberToHex, errorColor } from '~/util/util'
const props = defineProps<{
  darkColors?:any,
  mainColor?:string,
  lightColors?:any
}>()
</script>

<template>
  <!-- color blocks row -->
  <div class="w-1/1 flex mb-88px">
    <template v-for="color in props.darkColors">
      <ColorBlock :style="{'background':color}" :has-valid-color="isValidHex(numberToHex(props.mainColor))" :wide="false"/>
    </template>

    <ColorBlock :wide="true" :style="{ background: isValidHex(numberToHex(props.mainColor)) ? numberToHex(props.mainColor) : errorColor }" />

    <template v-for="color in props.lightColors">
      <ColorBlock :style="{'background':color}" :has-valid-color="isValidHex(numberToHex(props.mainColor))" :wide="false"/>
    </template>
  </div>
</template>

<style scoped>
</style>
