<script setup lang="ts">
import { ref } from 'vue'
import Color from 'color'

const props = defineProps<{
  hasValidColor?:boolean,
  color?:string,
  wide?:boolean
}>()

const maxWidth = ref(props.wide ? 192 : 72)
</script>

<template>
  <!-- color block container -->
  <div class="color-block-container" :style="{'max-width':maxWidth + 'px','min-width': props.wide ? maxWidth + 'px' : undefined}">
    <!-- color block code -->
    <div class="color-block-code">
      {{props.hasValidColor ? Color(props.color) : null }}
      <!-- copied text -->
      <div class="copied-text">{{Color(props.color).hex()}}</div>
    </div>
  </div>
</template>

<style scoped>
.color-block-code{
  position: absolute;
  top: 100%;
  padding-top: 8px;
  padding-bottom: 16px;
  transition: 0.2s
}
.color-block-container{
  position: relative;
  height: 72px;
  width: 100%;
  flex-shrink: 1;
  cursor: pointer;

  @media (max-width: 720px) {
    /* min-width: 96px; */
  }
}
.color-block-container:not(:hover) .color-block-code {
  opacity: 0;
  transition: .6s;
}
.copied-text{
  animation-duration: 0.8s;
  animation-name: copy-animation;
  opacity: 0;
}
@keyframes copy-animation{
  0% {
    opacity: 0;
    transform: translateY(-20px);
  }
  30% {
    opacity: 0.5;
  }
  70% {
    transform: translateY(0);
    opacity: 0.3;
  }
  100% {
    opacity: 0;
  }
}
</style>
