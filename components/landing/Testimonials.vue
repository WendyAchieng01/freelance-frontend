<template>
  <div class="testimonials-section py-16">
    <p class="text-h4 text-center mb-4 font-weight-bold primary--text">
      Trusted by Ambitious Brands <br />and Growing Startups
    </p>
    <p class="text-subtitle-1 text-center mb-12 grey--text text--darken-1">
      See how Kenyan and African businesses are scaling faster with NillTech
    </p>

    <v-row class="mt-6">
      <v-col
        v-for="(testimonial, index) in testimonials"
        :key="index"
        cols="12"
        md="6"
      >
        <v-sheet
          rounded="xl"
          elevation="2"
          class="pa-6 h-100 d-flex flex-column"
          color="grey lighten-4"
        >
          <div class="d-flex align-start mb-6">
            <v-avatar size="80" class="mr-4">
              <v-img
                :src="testimonial.image"
                cover
              />
            </v-avatar>

            <div>
              <p class="text-h6 font-weight-bold mb-1">
                {{ testimonial.name }}
              </p>
              <p class="text-subtitle-2 grey--text text--darken-2">
                {{ testimonial.role }} • {{ testimonial.company }}
              </p>
            </div>
          </div>

          <div class="flex-grow-1">
            <v-icon
              icon="mdi-format-quote-open"
              color="primary"
              size="32"
              class="quote-icon-start mb-2"
            />
            <p class="text-body-1 font-weight-medium">
              {{ testimonial.quote }}
            </p>
            <v-icon
              icon="mdi-format-quote-close"
              color="primary"
              size="32"
              class="quote-icon-end ml-2"
            />
          </div>

          <div class="mt-4">
            <v-rating
              v-model="rating"
              color="amber"
              background-color="grey lighten-1"
              length="5"
              size="20"
              readonly
              dense
            />
          </div>
        </v-sheet>
      </v-col>
    </v-row>


  </div>
</template>

<script setup>
const rating = 5

const testimonials = [
  {
    name: "Aisha Mwangi",
    role: "Founder & CEO",
    company: "Kipepeo Fashion",
    quote: "NillTech delivered our e-commerce mobile app and website in just 5 weeks. The quality and speed were unbelievable — our sales tripled in the first quarter!",
    image: "/images/testimonial_aisha.jpg" // Use professional smiling African female entrepreneur
  },
  {
    name: "Kevin Otieno",
    role: "Digital Marketing Lead",
    company: "SwiftGrow Agency",
    quote: "Their Microtask Marketplace saved us thousands. We get high-quality social media creatives, SEO tweaks, and content on-demand — faster and cheaper than hiring full-time.",
    image: "/images/testimonial_kevin.jpg" // Use confident young African male professional
  },
  {
    name: "Fatuma Ali",
    role: "Co-founder",
    company: "AfriLearn EdTech",
    quote: "From custom web app development to ongoing maintenance and hosting, NillTech has been our reliable tech partner. Professional, responsive, and truly understands African startups.",
    image: "/images/testimonial_fatuma.jpg" // Use warm smiling East African female business portrait
  },
  {
    name: "Brian Kamau",
    role: "Managing Director",
    company: "PeakPulse Logistics",
    quote: "We needed quick landing pages and micro-tasks for campaigns — NillTech delivered everything perfectly on tight deadlines. Best outsourcing decision we made this year.",
    image: "/images/testimonial_brian.jpg" // Use professional African male in business attire
  }
]
</script>

<style scoped>
.quote-icon-start,
.quote-icon-end {
  vertical-align: middle;
}

.testimonials-section {
  background: "#efefef";
}
</style>