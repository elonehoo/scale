<script setup lang="ts">
import Title from './Title.vue'
import Button from './Button.vue'
</script>

<template>
  <Title>Triggers</Title>
  <!-- button row -->
  <div class="button-row">
    <Button>Copy SVG</Button>

    <Button>Copy colors</Button>

    <Button>Randomize all</Button>

    <Button>Randomize color</Button>
  </div>
</template>

<style scoped>
.button-row{
  display: flex;
  flex-wrap: wrap;
}
.button-row > * {
  margin-right: 4px;

  @media (max-width: 720px) {
    margin-top: 4px;
  }
}
</style>
