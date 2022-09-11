<script setup lang="ts">
import Footer from '~/components/Footer.vue'
import BackgroundSelector from './components/BackgroundSelector.vue';
</script>

<template>
  <!-- main wrapper -->
  <div class="main-wrapper">
    <!-- top section -->
    <div class="top-section">
      <!-- colors section -->
      <div class="w-1/1">
        <!-- global config section -->
        <div class="global-config-section">
          <!-- background selector section -->
          <div class="background-selector-section">
            <BackgroundSelector />
          </div>
        </div>
      </div>
    </div>
  </div>
  <Footer />
</template>

<style scoped>
.main-wrapper{
  padding: 40px 80px;
  min-height: 100vh;
  display: flex;
  flex-direction: column;

  @media (max-width: 720px) {
    padding: 32px;
    min-height: calc(100vh - 40px);
  }
}
.top-section{
  flex: 1;
  display: flex;
  align-items: center;
}
.global-config-section{
  display: flex;
  margin-bottom: 64px;

  flex-wrap: wrap;
    @media (max-width: 1100px) {
  }
}
.background-selector-section{
  border-left: 1px solid var(--border);
  padding: 0 48px;
  height: 160px;

  @media (max-width: 720px) {
    padding: 16px 0;
    margin-top: 16px;
    border-left: 0;
    border-top: 1px solid var(--border);
  }
}
</style>
