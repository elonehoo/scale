<script setup lang="ts">
import DynamicInput from '~/components/DynamicInput.vue'
import Title from '~/components/Title.vue'
import { numberToHex } from '~/util/util'

const props = defineProps<{
  mainColor?:string,
  r?:number,
  g?:number,
  b?:number
}>()

defineEmits(['update:r','update:g','update:b','onInputBlur','update:mainColor'])

</script>

<template>
  <!-- input row -->
  <div class="input-row">
    <!-- inputs row item -->
    <div class="inputs-row-item">
      <DynamicInput :color="numberToHex(props.mainColor)" v-model:modelValue="props.mainColor" @update:modelValue="(e:any)=>{$emit('update:mainColor',e)}" @blur="$emit('onInputBlur')" prefix='#' label='Color' />
      <!-- slider wrapper -->
      <div class="flex items-center">
        <div class="mr-12px text-12px leading-16px font-700 relative top-2px">R</div>
        <input class="slider" type='range' @input="$emit('update:r', $event.target?.value)" min="0" max="255" :value="props.r" />
      </div>

      <!-- slider wrapper -->
      <div class="flex items-center">
        <div class="mr-12px text-12px leading-16px font-700 relative top-2px">G</div>
        <input class="slider" type='range' @input="$emit('update:g', $event.target?.value)" min="0" max="255" :value="props.g" />
      </div>

      <!-- slider wrapper -->
      <div class="flex items-center">
        <div class="mr-12px text-12px leading-16px font-700 relative top-2px">B</div>
        <input class="slider" type='range' @input="$emit('update:b', $event.target?.value)" min="0" max="255" :value="props.b" />
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

.slider{
  --thumbScale: 1;

  width: 96px;
  height: 12px;
  appearance: none;
  margin: 0;
  display: block;
  cursor: pointer;
  margin-top: 8px;
  margin-bottom: 8px;
  background-color: transparent;
}
.slider:focus {
  outline: none;
  --thumbScale: 1.2;
}
.slider::-webkit-slider-runnable-track {
  width: 100%;
  height: 2px;
  cursor: pointer;
  background: var(--bodyDimmed);
  border-radius: 2px;
}
.slider::-webkit-slider-thumb {
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
.slider::-moz-range-track {
  width: 100%;
  height: 2px;
  cursor: pointer;
  background: var(--bodyDimmed);
  border-radius: 2px;
}
.slider::-moz-range-thumb {
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
.slider::-ms-track {
  width: 100%;
  height: 2px;
  cursor: pointer;
  background: var(--bodyDimmed);
  border-radius: 2px;
}
.slider::-ms-fill-lower {
  background: #D8D8D8;
  border-radius: 2px;
}
.slider::-ms-fill-upper {
  background: #D8D8D8;
  border-radius: 2px;
}
.slider::-ms-thumb {
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
.slider:focus::-ms-fill-lower {
  background: #D8D8D8;
}
.slider:focus::-ms-fill-upper {
  background: #D8D8D8;
}
</style>
