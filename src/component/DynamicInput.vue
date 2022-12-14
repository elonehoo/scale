<script setup lang="ts">
import { ref } from 'vue'
import { isValidHex } from '~/util/util'
import Color from 'color'
import Slider from './Slider.vue'

const props = withDefaults(defineProps<{
  label?:string,
  prefix?:string,
  modelValue?:any,
  sufix?:string,
  min?:number,
  max?:number,
  withSlider?:boolean,
  color:string
}>(),({
  withSlider:false
}))

const emit = defineEmits(['update:modelValue','onChange'])

const selectionStyle = ref(isValidHex(props.color) ? Color(props.color).mix(Color('white'), 0.8).string() : '#666')
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
        <input type="text" :value="props.prefix" class="dynamic-input-field select-none opacity-40" @change="$emit('onChange')" tabindex={-1} />
        <div class="text-40px font-inherit leading-none opacity-0 transform-y">{{props.prefix}}</div>
      </div>

      <!-- input wrapper -->
      <div class="relative w-auto h-1/1">
        <!-- dynamic input field -->
        <input type="text" :value="props.modelValue" @input="$emit('update:modelValue',$event.target!.value)" class="dynamic-input-field select-none opacity-40" :min="props.min" :max="props.max" />
        <div class="text-40px font-inherit leading-none opacity-0 transform-y">{{props.modelValue}}</div>
      </div>

      <!-- input wrapper -->
      <div class="relative w-auto h-1/1">
        <!-- dynamic input field -->
        <input :value="props.sufix" class="dynamic-input-field select-none opacity-40" tabindex={-1} />
        <div class="text-40px font-inherit leading-none opacity-0 transform-y">{{props.sufix}}</div>
      </div>
    </div>
  </div>
  <template v-if="props.withSlider">
    <Slider type='range' :color="props.color" @change="emit('onChange')" v-model="props.modelValue" :min="props.min" :max="props.max"/>
  </template>
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
  appearance: none;
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
dynamic-input-field::-moz-selection {
  background: v-bind(selectionStyle);
}

dynamic-input-field::selection {
  background: v-bind(selectionStyle);
}
</style>
