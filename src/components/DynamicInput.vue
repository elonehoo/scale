<script setup lang="ts">
import { ref } from 'vue'
import { isValidHex } from '~/util/util'
const props = defineProps<{
  label?:string
}>()

const selectionStyle = ref()
</script>

<template>
  <div>
    <!-- dynamic-input-label -->
    <div class="text-12px font-700 leading-16px mb-16px min-h-32px">{{props.label}}</div>
    <!-- dynamic-input-root -->
    <div class="flex mb-16px">
      <!-- input wrapper -->
      <div class="relative w-auto h-1/1">
        <!-- dynamic input field -->
        <input type="text" class="dynamic-input-field select-none opacity-40" readonly tabindex={-1} />
        <div class="text-40px font-inherit leading-none opacity-0 transform-y"></div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.dynamic-input-field{
  color: inherit;
  font-size: 40px;
  font-family: inherit;
  font-weight: inherit;
  line-height: 1;
  padding: 0;
  border: 0;
  width: 100%;
  margin-right: 16px;
  position: absolute;
  top: 0;
  height: 100%;
  background-color: transparent;
  appearance: textfield;
  margin: 0;
}
.dynamic-input-field:focus {
  outline: none;
}
.dynamic-input-field::-webkit-outer-spin-button,
.dynamic-input-field::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
.dynamic-input-field::-moz-selection {
  background: v-bind(selectionStyle)
}
.dynamic-input-field::selection {
  background: v-bind(selectionStyle)
}
.transform-y{
  transform: translateY(236px) scale(0);
}
</style>
