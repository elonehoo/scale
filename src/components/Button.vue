<script setup lang="ts">

</script>

<template>
  <button class="button">
    <slot />
  </button>
</template>

<style scoped>
.button{
  appearance: none;
  border: none;
  font: inherit;
  color: inherit;
  background-color: var(--bodyXDimmed);
  padding: 0.4em 0.75em;
  cursor: pointer;
}
</style>
