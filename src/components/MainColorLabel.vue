<script setup lang="ts">

</script>

<template>
  <div class="relative w-auto h-1/1">
    <input
     type="text"
     class="text-inherit text-40px font-inherit family-inherit leading-none p-0px border-no w-1/1 h-1/1 absolute top-0px bg-inherit appearance-textfield ma-0px select-none opacity-40"
     readonly
     tabindex="-1"
     value="#" />
    <div class="text-40px font-inherit leading-none opacity-0 translate-y-236px">#</div>
  </div>
</template>

<style scoped>
.family-inherit{
  font-family: inherit;
}
.border-no{
  border: 0px;
}
.appearance-textfield{
  appearance: textfield;
}
.translate-y-236px{
  transform: translateY(236px) scale(0);
}
</style>
