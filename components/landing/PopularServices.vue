<template>
  <div class="popular-services-section py-16">
    <!-- Header Section -->
    <div class="header-container">
      <v-chip
        color="primary"
        label
        class="mb-4 px-6"
        text-color="white"
      >
        <v-icon left small>mdi-star</v-icon>
        What We Offer
      </v-chip>
      
      <h3 class="text-h3 text-center mb-3 font-weight-bold primary--text">
        Our Core Services
      </h3>
      <p class="text-h6 text-center mb-12 grey--text text--darken-1 mx-auto subtitle-text">
        From complex builds to quick digital tasks — we deliver work that moves businesses forward
      </p>
    </div>

    <v-row class="mt-8">
      <!-- Development Services Section -->
      <v-col cols="12">
        <div class="section-header mb-8">
          <v-icon color="primary" size="32" class="mr-3">mdi-code-braces</v-icon>
          <h4 class="text-h4 font-weight-bold primary--text d-inline">Development Services</h4>
        </div>
        
        <v-row>
          <v-col cols="12" sm="6" md="4">
            <ServiceCard
              title="Mobile & Web Apps"
              description="Custom mobile applications and powerful web applications built for scale"
              image="/images/service_website_developer.png"
              color="#e3f2fd"
              icon="mdi-cellphone-link"
            />
          </v-col>

          <v-col cols="12" sm="6" md="4">
            <ServiceCard
              title="Landing Pages & Websites"
              description="High-converting landing pages and modern, responsive websites"
              image="/images/service_technical_writer.png"
              color="#e8f5e9"
              icon="mdi-web"
            />
          </v-col>

          <v-col cols="12" sm="6" md="4">
            <ServiceCard
              title="Web Hosting & Maintenance"
              description="Reliable hosting, security updates, performance optimization & ongoing support"
              image="/images/service_graphic_designer.png"
              color="#fff3e0"
              icon="mdi-server-network"
            />
          </v-col>
        </v-row>
      </v-col>

      <!-- Microtask Marketplace -->
      <v-col cols="12" class="mt-16">
        <div class="section-header mb-8">
          <v-icon color="purple darken-2" size="32" class="mr-3">mdi-lightning-bolt</v-icon>
          <h4 class="text-h4 font-weight-bold purple--text text--darken-2 d-inline">
            Microtask Marketplace
          </h4>
        </div>
        
        <v-row justify="center">
          <v-col cols="12" md="10" lg="9">
            <v-card
              rounded="xl"
              elevation="8"
              class="marketplace-card overflow-hidden"
            >
              <div class="gradient-bg pa-10">
                <v-row align="center">
                  <v-col cols="12" md="5" class="text-center text-md-left">
                    <div class="icon-wrapper mb-6">
                      <v-icon size="80" color="white">
                        mdi-clock-fast
                      </v-icon>
                    </div>

                    <h5 class="text-h4 font-weight-bold white--text mb-4">
                      Fast Turnaround Digital Tasks
                    </h5>

                    <p class="text-h6 white--text mb-6 font-weight-light">
                      Outsource-ready micro-tasks with on-demand freelance workforce
                    </p>

                    <v-btn
                      color="white"
                      x-large
                      rounded
                      class="mt-4 px-8 purple--text text--darken-2 font-weight-bold"
                      elevation="0"
                      :to="{ path: '/microtasks' }"
                    >
                      Explore Marketplace
                      <v-icon right>mdi-arrow-right</v-icon>
                    </v-btn>
                  </v-col>

                  <v-col cols="12" md="7">
                    <v-card
                      rounded="lg"
                      class="pa-6 mt-6 mt-md-0"
                      elevation="0"
                    >
                      <p class="text-subtitle-1 mb-4 grey--text text--darken-2 font-weight-medium">
                        Popular Tasks:
                      </p>
                      
                      <div class="chip-container">
                        <v-chip
                          v-for="(task, index) in popularTasks"
                          :key="index"
                          class="ma-1 chip-hover"
                          :color="task.color"
                          label
                          large
                        >
                          <v-icon left small>{{ task.icon }}</v-icon>
                          {{ task.name }}
                        </v-chip>
                        
                        <v-chip
                          class="ma-1"
                          color="grey lighten-2"
                          label
                          large
                        >
                          <v-icon left small>mdi-plus</v-icon>
                          50+ More
                        </v-chip>
                      </div>

                      <v-divider class="my-6"></v-divider>

                      <v-row class="text-center">
                        <v-col cols="4">
                          <div class="stat-item">
                            <h6 class="text-h5 font-weight-bold primary--text">5k+</h6>
                            <p class="text-caption grey--text">Active Tasks</p>
                          </div>
                        </v-col>
                        <v-col cols="4">
                          <div class="stat-item">
                            <h6 class="text-h5 font-weight-bold primary--text">24h</h6>
                            <p class="text-caption grey--text">Avg. Delivery</p>
                          </div>
                        </v-col>
                        <v-col cols="4">
                          <div class="stat-item">
                            <h6 class="text-h5 font-weight-bold primary--text">98%</h6>
                            <p class="text-caption grey--text">Satisfaction</p>
                          </div>
                        </v-col>
                      </v-row>
                    </v-card>
                  </v-col>
                </v-row>
              </div>
            </v-card>
          </v-col>
        </v-row>
      </v-col>
    </v-row>

    <!-- CTA Section -->
    <div class="cta-section text-center mt-16 pa-8">
      <h5 class="text-h5 mb-4 font-weight-medium">
        Ready to get started?
      </h5>
      <p class="text-subtitle-1 grey--text text--darken-1 mb-6">
        Join thousands of businesses already working with talented professionals
      </p>
      <v-btn
        color="primary"
        x-large
        rounded
        class="px-12 text-subtitle-1 font-weight-bold"
        elevation="8"
        :to="{ path: '/auth/register' }"
      >
        Hire Amazing Talents Now
        <v-icon right>mdi-rocket-launch</v-icon>
      </v-btn>
    </div>
  </div>
</template>

<script setup>
import ServiceCard from '@/components/landing/ServiceCard.vue'

const popularTasks = [
  { name: 'Logo Design', icon: 'mdi-palette', color: 'blue lighten-4' },
  { name: 'Content Writing', icon: 'mdi-pencil', color: 'green lighten-4' },
  { name: 'Social Media', icon: 'mdi-share-variant', color: 'pink lighten-4' },
  { name: 'SEO', icon: 'mdi-google', color: 'orange lighten-4' },
  { name: 'Graphics', icon: 'mdi-image-edit', color: 'purple lighten-4' },
  { name: 'Video Editing', icon: 'mdi-video', color: 'red lighten-4' }
]
</script>

<style scoped>
.popular-services-section {
  background: linear-gradient(180deg, #fafbfc 0%, #ffffff 50%, #f8f9fa 100%);
  position: relative;
}

.header-container {
  text-align: center;
  position: relative;
  z-index: 1;
}

.subtitle-text {
  max-width: 700px;
}

.section-header {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 2rem;
}

.marketplace-card {
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.marketplace-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 12px 40px rgba(0, 0, 0, 0.15) !important;
}

.gradient-bg {
  background: linear-gradient(135deg, #5281b7 0%, #5ca9e8 100%);
  position: relative;
  overflow: hidden;
}

.icon-wrapper {
  display: inline-block;
  padding: 20px;
  background: rgba(255, 255, 255, 0.2);
  border-radius: 50%;
  backdrop-filter: blur(10px);
}

.chip-container {
  display: flex;
  flex-wrap: wrap;
  gap: 4px;
}

.chip-hover {
  transition: transform 0.2s ease, box-shadow 0.2s ease;
  cursor: pointer;
}

.chip-hover:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

.stat-item {
  padding: 0.5rem;
}

.cta-section {
  background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
  border-radius: 20px;
  max-width: 900px;
  margin: 0 auto;
  position: relative;
  overflow: hidden;
}

.cta-section::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: url("data:image/svg+xml,%3Csvg width='60' height='60' viewBox='0 0 60 60' xmlns='http://www.w3.org/2000/svg'%3E%3Cg fill='none' fill-rule='evenodd'%3E%3Cg fill='%239C92AC' fill-opacity='0.05'%3E%3Cpath d='M36 34v-4h-2v4h-4v2h4v4h2v-4h4v-2h-4zm0-30V0h-2v4h-4v2h4v4h2V6h4V4h-4zM6 34v-4H4v4H0v2h4v4h2v-4h4v-2H6zM6 4V0H4v4H0v2h4v4h2V6h4V4H6z'/%3E%3C/g%3E%3C/g%3E%3C/svg%3E");
  opacity: 0.4;
}

@media (max-width: 960px) {
  .section-header {
    flex-direction: column;
    text-align: center;
  }
  
  .section-header h4 {
    margin-top: 0.5rem;
  }
}
</style>