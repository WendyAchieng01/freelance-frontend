<template>
  <div id="faq" class="py-16">
    <p class="text-h4 text-center font-weight-bold primary--text mb-4">
      Frequently Asked Questions
    </p>
    <p class="text-subtitle-1 text-center grey--text text--darken-1 mb-12">
      Everything you need to know about working with NillTech Solutions
    </p>

    <v-expansion-panels
      class="mt-8"
      rounded="lg"
      variant="accordion"
      flat
    >
      <v-expansion-panel
        v-for="(item, index) in faqItems"
        :key="index"
        class="mb-4 elevation-1 rounded-lg"
      >
        <v-expansion-panel-title class="py-4">
          <p class="text-subtitle-1 font-weight-medium">
            {{ item.question }}
          </p>
        </v-expansion-panel-title>

        <v-expansion-panel-text class="px-6 pb-6 text-body-1">
          <div v-html="item.answer"></div>
        </v-expansion-panel-text>
      </v-expansion-panel>
    </v-expansion-panels>

    <div class="text-center mt-12">
      <p class="text-body-1 grey--text text--darken-2 mb-4">
        Still have questions?
      </p>
      <v-btn
        color="primary"
        size="large"
        class="px-10"
        :href="`mailto:info@nitechsolutions.com?subject=Question%20about%20NillTech%20Services`"
      >
        Contact Us Directly
      </v-btn>
    </div>
  </div>
</template>

<script setup>
const faqItems = [
  {
    question: "What kind of services does NillTech Solutions provide?",
    answer: `We offer two main ways to work with us:<br><br>
    <strong>1. Long-term Development Projects</strong><br>
    • Custom Mobile Apps (Android & iOS)<br>
    • Web Applications & Websites<br>
    • High-converting Landing Pages<br>
    • Web Hosting, Domain, SSL & Ongoing Maintenance<br><br>
    <strong>2. Microtask Marketplace</strong><br>
    Fast, on-demand digital tasks like logo design, social media creatives, content writing, SEO optimization, video editing, graphic design edits, and many more.`
  },
  {
    question: "How much do your services cost?",
    answer: `Pricing is project-based and very flexible.<br><br>
    • Long-term projects: We provide detailed quotes after understanding your requirements (usually KSh 150,000 – 2,500,000+ depending on complexity)<br>
    • Microtasks: Most tasks range from KSh 1,500 – KSh 35,000 with transparent pricing shown before you start<br><br>
    We always aim to be competitive while delivering high-quality work.`
  },
  {
    question: "How fast can you deliver my project or task?",
    answer: `Speed depends on scope:<br><br>
    • Microtasks: Most are completed in 24–72 hours (some same-day)<br>
    • Landing pages & small websites: 5–14 days<br>
    • Full custom web/mobile apps: 6–16 weeks (with clear milestones)<br><br>
    We’re known for fast turnarounds compared to traditional agencies.`
  },
  {
    question: "Do you work with startups and small businesses in Kenya?",
    answer: `Yes — absolutely!<br><br>
    Most of our clients are Kenyan startups, SMEs, digital agencies, e-commerce brands, edtech, agritech, fintech, and creative entrepreneurs.<br>
    We understand tight budgets, fast growth needs, and the realities of the Kenyan/East African market.`
  },
  {
    question: "What happens after the project is delivered?",
    answer: `• Long-term projects include 30–90 days of free bug fixes & support (depending on package)<br>
    • We offer affordable monthly maintenance & hosting packages<br>
    • Microtasks come with 1–2 revision rounds included<br><br>
    We want long-term relationships — many clients keep coming back for more tasks and projects!`
  },
  {
    question: "How do I get started?",
    answer: `Very simple:<br><br>
    1. Send us your requirements via WhatsApp, email or the contact form<br>
    2. We’ll have a quick call/brief discussion<br>
    3. You receive a clear proposal/quote<br>
    4. Work begins after 30–50% deposit (flexible for trusted clients)<br><br>
    We can start small with a quick microtask to test our quality!`
  }
]
</script>

<style scoped>
/* Optional: enhance panel look */
.v-expansion-panel {
  border-radius: 12px !important;
  overflow: hidden;
  margin-bottom: 16px;
}

.v-expansion-panel-title {
  background-color: #f8f9fa;
}

.v-expansion-panel--active .v-expansion-panel-title {
  background-color: var(--v-primary-base) !important;
  color: white !important;
}
</style>