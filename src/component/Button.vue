<script setup lang="ts">

</script>

<template>
  <button>
    <slot />
  </button>
</template>

<style scoped>
button{
  appearance: none;
  border: none;
  font: inherit;
  color: inherit;
  background-color: var(--bodyXDimmed);
  padding: 0.4em 0.75em;
  cursor: pointer;
}
button:focus {
  outline: none;
  background-color: var(--bodyDimmed);
}
button:active {
  background-color: var(--bodyColor);
}
</style>
