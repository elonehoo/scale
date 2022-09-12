<script setup lang="ts">

</script>

<template>
  <!-- input row -->
  <div class="input-row">
    <!-- inputs row item -->
    <div class="inputs-row-item">

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
