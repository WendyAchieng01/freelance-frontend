<template>
  <div class="portfolio-section py-12">
    <!-- Header -->
    <div class="text-center mb-10">
      <p class="text-overline text-primary font-weight-bold mb-2">
        Our Impact
      </p>
      <h3 class="text-h4 font-weight-bold grey--text text--darken-3 mb-3">
        Companies we helped grow
      </h3>
      <p class="text-subtitle-1 grey--text">
        Trusted by innovative companies worldwide
      </p>
    </div>

    <!-- Company Logos Grid -->
    <v-row class="mt-8" justify="center">
      <v-col
        v-for="(company, index) in companies"
        :key="index"
        cols="6"
        sm="4"
        md="3"
        lg="2"
      >
        <v-card
          elevation="0"
          rounded="lg"
          class="company-card pa-6 d-flex align-center justify-center"
          hover
        >
          <div class="company-logo-wrapper">
            <!-- Using SVG placeholder logos with company initials -->
            <div class="company-logo" :style="{ background: company.color }">
              <span class="company-initial white--text">
                {{ company.initial }}
              </span>
            </div>
            <p class="text-caption text-center mt-2 grey--text text--darken-1 font-weight-medium">
              {{ company.name }}
            </p>
          </div>
        </v-card>
      </v-col>
    </v-row>

    <!-- Stats Bar -->
    <v-row class="mt-12" justify="center">
      <v-col cols="12" md="10">
        <v-card
          rounded="xl"
          elevation="2"
          class="stats-bar pa-6"
          color="grey lighten-4"
        >
          <v-row align="center" justify="center">
            <v-col
              v-for="(stat, index) in stats"
              :key="index"
              cols="6"
              md="3"
              class="text-center stat-item"
            >
              <div class="stat-content">
                <v-icon :color="stat.color" size="32" class="mb-2">
                  {{ stat.icon }}
                </v-icon>
                <h5 class="text-h4 font-weight-bold text-primary mb-1">
                  {{ stat.value }}
                </h5>
                <p class="text-caption text-medium-emphasis">
                  {{ stat.label }}
                </p>
              </div>
            </v-col>
          </v-row>
        </v-card>
      </v-col>
    </v-row>

    <!-- Featured Project Showcase -->
    <v-row class="mt-12">
      <v-col cols="12">
        <h4 class="text-h5 font-weight-bold text-center mb-8 grey--text text--darken-3">
          Featured Success Stories
        </h4>
      </v-col>
      
      <v-col
        v-for="(project, index) in featuredProjects"
        :key="index"
        cols="12"
        md="6"
      >
        <v-card
          rounded="xl"
          elevation="4"
          class="project-card overflow-hidden"
          hover
        >
          <!-- Project Image/Icon -->
          <div class="project-header" :style="{ background: project.gradient }">
            <v-icon size="80" color="white" class="project-icon">
              {{ project.icon }}
            </v-icon>
          </div>

          <!-- Project Details -->
          <v-card-text class="pa-6">
            <div class="d-flex align-center mb-3">
              <v-chip
                small
                :color="project.chipColor"
                text-color="white"
                class="mr-2"
              >
                {{ project.category }}
              </v-chip>
              <v-chip small outlined>
                {{ project.duration }}
              </v-chip>
            </div>

            <h5 class="text-h6 font-weight-bold mb-3">
              {{ project.title }}
            </h5>

            <p class="text-body-2 grey--text text--darken-1 mb-4">
              {{ project.description }}
            </p>

            <!-- Results -->
            <v-divider class="mb-4"></v-divider>
            <div class="results-grid">
              <div
                v-for="(result, idx) in project.results"
                :key="idx"
                class="result-item"
              >
                <p class="text-h6 font-weight-bold primary--text mb-0">
                  {{ result.value }}
                </p>
                <p class="text-caption grey--text">
                  {{ result.label }}
                </p>
              </div>
            </div>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const companies = ref([
  { name: 'TechCorp', initial: 'TC', color: 'linear-gradient(135deg, #667eea 0%, #764ba2 100%)' },
  { name: 'StartupHub', initial: 'SH', color: 'linear-gradient(135deg, #f093fb 0%, #f5576c 100%)' },
  { name: 'InnovateLab', initial: 'IL', color: 'linear-gradient(135deg, #4facfe 0%, #00f2fe 100%)' },
  { name: 'GrowthCo', initial: 'GC', color: 'linear-gradient(135deg, #43e97b 0%, #38f9d7 100%)' },
  { name: 'DigitalEdge', initial: 'DE', color: 'linear-gradient(135deg, #fa709a 0%, #fee140 100%)' },
  { name: 'CloudSync', initial: 'CS', color: 'linear-gradient(135deg, #30cfd0 0%, #330867 100%)' }
])

const stats = ref([
  { icon: 'mdi-briefcase-check', value: '500+', label: 'Projects Delivered', color: 'grey darken-4' },
  { icon: 'mdi-domain', value: '200+', label: 'Companies Served', color: 'grey darken-4' },
  { icon: 'mdi-earth', value: '35+', label: 'Countries', color: 'grey darken-4' },
  { icon: 'mdi-account-star', value: '98%', label: 'Satisfaction Rate', color: 'grey darken-4' }
])

const featuredProjects = ref([
  {
    title: 'E-Commerce Platform Redesign',
    category: 'Web Development',
    duration: '3 months',
    description: 'Complete overhaul of an e-commerce platform for a leading retail brand, focusing on user experience and conversion optimization.',
    icon: 'mdi-shopping',
    gradient: 'linear-gradient(135deg, #667eea 0%, #764ba2 100%)',
    chipColor: 'primary',
    results: [
      { value: '+185%', label: 'Sales Growth' },
      { value: '2.5x', label: 'Faster Load' },
      { value: '+240%', label: 'Mobile Traffic' }
    ]
  },
  {
    title: 'Mobile App Development',
    category: 'Mobile Development',
    duration: '4 months',
    description: 'Built a cross-platform mobile application for a fintech startup, enabling seamless financial management on the go.',
    icon: 'mdi-cellphone-link',
    gradient: 'linear-gradient(135deg, #4facfe 0%, #00f2fe 100%)',
    chipColor: 'info',
    results: [
      { value: '50K+', label: 'Downloads' },
      { value: '4.8★', label: 'App Rating' },
      { value: '85%', label: 'Retention Rate' }
    ]
  }
])
</script>

<style scoped>
.portfolio-section {
  background: linear-gradient(180deg, #ffffff 0%, #f8f9fa 100%);
}

.company-card {
  transition: all 0.3s ease;
  background: white;
  border: 2px solid transparent;
  min-height: 120px;
}

.company-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.1) !important;
  border-color: rgba(var(--v-primary-base), 0.2);
}

.company-logo-wrapper {
  width: 100%;
  text-align: center;
}

.company-logo {
  width: 64px;
  height: 64px;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
  transition: transform 0.3s ease;
}

.company-card:hover .company-logo {
  transform: scale(1.1) rotate(5deg);
}

.company-initial {
  font-size: 24px;
  font-weight: bold;
}

.stats-bar {
  background: white !important;
  border: 2px solid #e0e0e0;
}

.stat-item {
  position: relative;
}

.stat-item:not(:last-child)::after {
  content: '';
  position: absolute;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
  height: 60%;
  width: 1px;
  background: #e0e0e0;
}

.stat-content {
  transition: transform 0.3s ease;
}

.stat-item:hover .stat-content {
  transform: scale(1.05);
}

.project-card {
  transition: all 0.3s ease;
  border: 2px solid transparent;
}

.project-card:hover {
  transform: translateY(-6px);
  box-shadow: 0 12px 40px rgba(0, 0, 0, 0.15) !important;
  border-color: rgba(var(--v-primary-base), 0.3);
}

.project-header {
  height: 200px;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  overflow: hidden;
}

.project-header::before {
  content: '';
  position: absolute;
  top: -50%;
  right: -50%;
  width: 200%;
  height: 200%;
  background: radial-gradient(circle, rgba(255,255,255,0.2) 0%, transparent 70%);
  animation: pulse 8s ease-in-out infinite;
}

.project-icon {
  position: relative;
  z-index: 1;
  transition: transform 0.3s ease;
}

.project-card:hover .project-icon {
  transform: scale(1.1) rotate(10deg);
}

.results-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
}

.result-item {
  text-align: center;
  padding: 8px;
  background: rgba(var(--v-primary-base), 0.05);
  border-radius: 8px;
  transition: all 0.3s ease;
}

.result-item:hover {
  background: rgba(var(--v-primary-base), 0.1);
  transform: translateY(-2px);
}

@keyframes pulse {
  0%, 100% {
    transform: translate(0, 0) scale(1);
  }
  50% {
    transform: translate(-10%, -10%) scale(1.1);
  }
}

/* Responsive Design */
@media (max-width: 960px) {
  .stat-item::after {
    display: none;
  }
  
  .results-grid {
    grid-template-columns: repeat(3, 1fr);
    gap: 8px;
  }
}

@media (max-width: 600px) {
  .company-logo {
    width: 56px;
    height: 56px;
  }
  
  .company-initial {
    font-size: 20px;
  }
  
  .results-grid {
    grid-template-columns: 1fr;
  }
}
</style>