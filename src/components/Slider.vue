<script setup lang="ts">

</script>

<template>
  <input class="slider" />
</template>

<style scoped>
.slider{
  --thumbScale: 1;

  width: 96px;
  height: 12px;
  -webkit-appearance: none;
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
  -webkit-appearance: none;
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
  -webkit-appearance: none;
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
  -webkit-appearance: none;
  margin-top: -4px;
}
.slider:focus::-ms-fill-lower {
  background: #D8D8D8;
}
.slider:focus::-ms-fill-upper {
  background: #D8D8D8;
}
</style>
