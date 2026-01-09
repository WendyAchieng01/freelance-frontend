<template>
  <v-card
    rounded="xl"
    elevation="2"
    class="service-card h-100 d-flex flex-column"
    hover
    @mouseenter="isHovered = true"
    @mouseleave="isHovered = false"
  >
    <!-- Image Section with Overlay -->
    <div class="image-container">
      <v-sheet
        :color="color"
        height="200"
        class="d-flex justify-center align-center rounded-t-xl position-relative overflow-hidden"
      >
        <div class="image-backdrop" :class="{ 'hovered': isHovered }"></div>
        
        <v-img
          :src="image"
          height="140"
          width="140"
          contain
          class="service-image"
          :class="{ 'hovered': isHovered }"
        />
        
        <!-- Floating Icon Badge -->
        <div class="icon-badge" :class="{ 'hovered': isHovered }">
          <v-icon color="white" size="24">{{ icon }}</v-icon>
        </div>
      </v-sheet>
    </div>

    <!-- Content Section -->
    <v-card-title class="text-h6 font-weight-bold pt-6 pb-2 px-6">
      {{ title }}
    </v-card-title>

    <v-card-text class="flex-grow-1 px-6 pb-6">
      <p class="text-body-1 grey--text text--darken-2 mb-4">
        {{ description }}
      </p>

      <!-- Feature Tags -->
      <div class="feature-tags mt-auto">
        <v-chip
          x-small
          outlined
          class="mr-1 mb-1"
          color="primary"
        >
          Professional
        </v-chip>
        <v-chip
          x-small
          outlined
          class="mr-1 mb-1"
          color="success"
        >
          Fast Delivery
        </v-chip>
      </div>
    </v-card-text>

  </v-card>
</template>

<script setup>
import { ref } from 'vue'

defineProps({
  title: String,
  description: String,
  image: String,
  color: String,
  icon: {
    type: String,
    default: 'mdi-star'
  }
})

const isHovered = ref(false)
</script>

<style scoped>
.service-card {
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  border: 2px solid transparent;
  position: relative;
  overflow: hidden;
}

.service-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 12px 40px rgba(0, 0, 0, 0.12) !important;
  border-color: rgba(var(--v-primary-base), 0.3);
}

.image-container {
  position: relative;
  overflow: hidden;
}

.image-backdrop {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: radial-gradient(circle at center, rgba(255, 255, 255, 0.3) 0%, transparent 70%);
  opacity: 0;
  transition: opacity 0.4s ease;
  pointer-events: none;
}

.image-backdrop.hovered {
  opacity: 1;
}

.service-image {
  transition: transform 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  z-index: 1;
}

.service-image.hovered {
  transform: scale(1.1) rotate(3deg);
}

.icon-badge {
  position: absolute;
  top: 16px;
  right: 16px;
  width: 48px;
  height: 48px;
  background: linear-gradient(135deg, rgba(var(--v-primary-base), 0.9) 0%, rgba(var(--v-primary-base), 0.7) 100%);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
  z-index: 2;
  transition: all 0.3s ease;
  transform: scale(0.9);
  opacity: 0.9;
}

.icon-badge.hovered {
  transform: scale(1) rotate(360deg);
  opacity: 1;
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.25);
}

.feature-tags {
  margin-top: auto;
}

.slide-in {
  transition: all 0.3s ease;
}

.arrow-animate {
  transition: transform 0.3s ease;
  display: inline-block;
}

.service-card:hover .arrow-animate {
  transform: translateX(4px);
}

/* Shimmer effect on hover */
.service-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(
    90deg,
    transparent,
    rgba(255, 255, 255, 0.3),
    transparent
  );
  transition: left 0.5s ease;
  pointer-events: none;
  z-index: 1;
}

.service-card:hover::before {
  left: 100%;
}

/* Responsive adjustments */
@media (max-width: 600px) {
  .service-image {
    height: 120px !important;
    width: 120px !important;
  }
  
  .icon-badge {
    width: 40px;
    height: 40px;
  }
  
  .icon-badge .v-icon {
    font-size: 20px !important;
  }
}
</style>