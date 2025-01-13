<script setup lang="ts">
defineProps<{
  loading: boolean
}>()
</script>

<template>
  <div class="loading-wrapper">
    <transition name="fade" mode="out-in">
      <div v-if="loading" class="skeleton-container">
        <div class="skeleton-content">
          <div class="skeleton-line"></div>
          <div class="skeleton-line"></div>
          <div class="skeleton-line short"></div>
          <LoadSpinner class="spinner-overlay" />
        </div>
      </div>
      <div v-else class="content-container">
        <slot />
      </div>
    </transition>
  </div>
</template>

<style scoped>
.loading-wrapper {
  width: 100%;
  min-height: 200px;
  position: relative;
}

.skeleton-container {
  padding: var(--space-md, 1rem);
  background: var(--bg-card, #fff);
  border-radius: var(--radius-lg, 12px);
  box-shadow: var(--shadow-sm);
}

.skeleton-content {
  position: relative;
}

.skeleton-line {
  height: 1rem;
  background: linear-gradient(90deg, #f0f0f0 25%, #e0e0e0 50%, #f0f0f0 75%);
  background-size: 200% 100%;
  animation: shimmer 1.5s infinite;
  border-radius: var(--radius-sm, 6px);
  margin-bottom: var(--space-sm, 0.75rem);
}

.skeleton-line.short {
  width: 60%;
}

@keyframes shimmer {
  0% {
    background-position: 200% 0;
  }
  100% {
    background-position: -200% 0;
  }
}

.spinner-overlay {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.content-container {
  width: 100%;
}

/* Fade transition */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease, transform 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateY(10px);
}

/* Responsive design */
@media (max-width: 768px) {
  .loading-wrapper {
    min-height: 150px;
  }
  
  .skeleton-container {
    padding: var(--space-sm, 0.75rem);
  }
  
  .skeleton-line {
    height: 0.875rem;
    margin-bottom: var(--space-xs, 0.5rem);
  }
}

@media (max-width: 480px) {
  .loading-wrapper {
    min-height: 120px;
  }
  
  .skeleton-line {
    height: 0.75rem;
  }
}
</style>