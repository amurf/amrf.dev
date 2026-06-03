<script setup lang="ts">
import { ref, onMounted } from 'vue'

// --- Profile & Link Constants ---
const kofiProfileUrl = ref('https://ko-fi.com/amurf') 
const githubUrl = ref('https://github.com/amurf')
const linkedinUrl = ref('https://www.linkedin.com/in/ashmurf/')
const contactEmail = ref('self@amrf.dev')

// --- Toggle Ko-Fi Button ---
// Change to true to show the floating Ko-Fi button by default.
// You can also preview/override it by adding '?kofi=true' or '?kofi=false' to the URL.
const showKofi = ref(false)

onMounted(() => {
  const params = new URLSearchParams(window.location.search)
  if (params.has('kofi')) {
    showKofi.value = params.get('kofi') === 'true'
  }
})
</script>

<template>
  <div class="container">
    <!-- Hero Header -->
    <header class="hero">
      <h1>Ashley Murphy</h1>
      <p class="tagline">Senior Software Engineer</p>
      
      <div class="social-links">
        <a :href="githubUrl" target="_blank" rel="noopener noreferrer" class="btn-pill">
          <svg viewBox="0 0 24 24" width="16" height="16" fill="currentColor" aria-hidden="true">
            <path d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.53 1.032 1.53 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0022 12.017C22 6.484 17.522 2 12 2z"/>
          </svg>
          GitHub
        </a>
        <a :href="linkedinUrl" target="_blank" rel="noopener noreferrer" class="btn-pill">
          <svg viewBox="0 0 24 24" width="16" height="16" fill="currentColor" aria-hidden="true">
            <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
          </svg>
          LinkedIn
        </a>
        <a :href="'mailto:' + contactEmail" class="btn-pill">
          <svg viewBox="0 0 24 24" width="16" height="16" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
            <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/>
            <polyline points="22,6 12,13 2,6"/>
          </svg>
          Email
        </a>
      </div>
    </header>

    <main>
      <!-- Projects Showcase -->
      <section id="projects">
        <h2>projects</h2>
        <div class="apps-grid">
          <!-- Project 1: Alphabetical -->
          <div class="app-card">
            <div class="app-badge">iOS & Android App (Upcoming)</div>
            <h3 class="app-title">Alphabetical</h3>
            
            <!-- Project Image Mockup -->
            <div class="project-image-container">
              <img src="/alphabetical_mockup.png" alt="Alphabetical Word Puzzle App Mockup" class="project-image" />
            </div>
            
            <p class="app-description">
              A fast-paced verbal word puzzle and ordering game designed to test cognitive agility and alphabetical reflexes. Solve grids, race the timer, and compete globally.
            </p>

            <div class="project-links">
              <a href="#" target="_blank" rel="noopener noreferrer" class="btn-pill btn-store">
                <svg viewBox="0 0 24 24" width="14" height="14" fill="currentColor" aria-hidden="true">
                  <path d="M18.71 19.5c-.83 1.24-1.71 2.45-3.05 2.47-1.34.03-1.77-.79-3.29-.79-1.53 0-2 .77-3.27.82-1.31.05-2.3-1.32-3.14-2.53C4.25 17 2.94 12.45 4.7 9.39c.87-1.52 2.43-2.48 4.12-2.51 1.28-.02 2.5.87 3.29.87.78 0 2.26-1.07 3.81-.91.65.03 2.47.26 3.64 1.98-.09.06-2.17 1.28-2.15 3.81.03 3.02 2.65 4.03 2.68 4.04-.03.07-.42 1.44-1.38 2.83M15.97 4.17c.66-.81 1.11-1.93.99-3.06-1 .04-2.21.67-2.93 1.49-.62.69-1.16 1.84-1.01 2.96 1.12.09 2.27-.57 2.95-1.39z"/>
                </svg>
                App Store
              </a>
              <a href="#" target="_blank" rel="noopener noreferrer" class="btn-pill btn-store">
                <svg viewBox="0 0 24 24" width="14" height="14" fill="currentColor" aria-hidden="true">
                  <path d="M5.25 3.062c-.276 0-.528.093-.72.247l11.455 11.455L20.4 12.24c.732-.408.732-1.072 0-1.48L5.94 3.284a1.053 1.053 0 0 0-.69-.222zm-.96.883c-.046.13-.07.275-.07.43v15.25c0 .155.024.3.07.43L15.225 12 4.29 3.945zm12.42 11.835L5.255 20.69c.192.154.444.247.72.247.24 0 .473-.08.69-.202l14.46-7.48-4.44-2.36z"/>
                </svg>
                Google Play
              </a>
            </div>
          </div>

          <!-- Project 2: Calculator Game -->
          <div class="app-card">
            <div class="app-badge">iOS & Android App (Upcoming)</div>
            <h3 class="app-title">Calculator Game</h3>
            
            <!-- Project Image Mockup -->
            <div class="project-image-container">
              <img src="/calculator_mockup.png" alt="Calculator Game App Mockup" class="project-image" />
            </div>
            
            <p class="app-description">
              A minimalistic mathematical logic puzzle. Use a limited set of calculator operators to manipulate the starting value and hit the target number. Simple rules, deep strategies.
            </p>

            <div class="project-links">
              <a href="#" target="_blank" rel="noopener noreferrer" class="btn-pill btn-store">
                <svg viewBox="0 0 24 24" width="14" height="14" fill="currentColor" aria-hidden="true">
                  <path d="M18.71 19.5c-.83 1.24-1.71 2.45-3.05 2.47-1.34.03-1.77-.79-3.29-.79-1.53 0-2 .77-3.27.82-1.31.05-2.3-1.32-3.14-2.53C4.25 17 2.94 12.45 4.7 9.39c.87-1.52 2.43-2.48 4.12-2.51 1.28-.02 2.5.87 3.29.87.78 0 2.26-1.07 3.81-.91.65.03 2.47.26 3.64 1.98-.09.06-2.17 1.28-2.15 3.81.03 3.02 2.65 4.03 2.68 4.04-.03.07-.42 1.44-1.38 2.83M15.97 4.17c.66-.81 1.11-1.93.99-3.06-1 .04-2.21.67-2.93 1.49-.62.69-1.16 1.84-1.01 2.96 1.12.09 2.27-.57 2.95-1.39z"/>
                </svg>
                App Store
              </a>
              <a href="#" target="_blank" rel="noopener noreferrer" class="btn-pill btn-store">
                <svg viewBox="0 0 24 24" width="14" height="14" fill="currentColor" aria-hidden="true">
                  <path d="M5.25 3.062c-.276 0-.528.093-.72.247l11.455 11.455L20.4 12.24c.732-.408.732-1.072 0-1.48L5.94 3.284a1.053 1.053 0 0 0-.69-.222zm-.96.883c-.046.13-.07.275-.07.43v15.25c0 .155.024.3.07.43L15.225 12 4.29 3.945zm12.42 11.835L5.255 20.69c.192.154.444.247.72.247.24 0 .473-.08.69-.202l14.46-7.48-4.44-2.36z"/>
                </svg>
                Google Play
              </a>
            </div>
          </div>
        </div>
      </section>

      <!-- Work Experience Timeline -->
      <section id="experience">
        <h2>experience</h2>
        <div class="exp-list">
          <!-- Okendo -->
          <div class="exp-item active">
            <div class="exp-header">
              <span class="exp-role">Senior Software Engineer</span>
              <span class="exp-date">Jan 2025 - Present</span>
            </div>
            <div class="exp-company">Okendo</div>
            <div class="exp-tech">
              <span class="tech-tag">Serverless</span>
              <span class="tech-tag">Lambda</span>
              <span class="tech-tag">SQS</span>
              <span class="tech-tag">API Gateway</span>
              <span class="tech-tag">Cognito</span>
              <span class="tech-tag">DynamoDB</span>
              <span class="tech-tag">Redshift</span>
              <span class="tech-tag">Elasticsearch</span>
              <span class="tech-tag">Vue 3</span>
              <span class="tech-tag">React</span>
              <span class="tech-tag">Remix</span>
              <span class="tech-tag">Angular</span>
              <span class="tech-tag">Shopify</span>
              <span class="tech-tag">TypeScript</span>
              <span class="tech-tag">D3</span>
              <span class="tech-tag">Puppeteer</span>
              <span class="tech-tag">Terraform</span>
            </div>
          </div>

          <!-- Megaport -->
          <div class="exp-item">
            <div class="exp-header">
              <span class="exp-role">Senior Frontend Engineer</span>
              <span class="exp-date">Jan 2021 - Jan 2025</span>
            </div>
            <div class="exp-company">Megaport</div>
            <div class="exp-tech">
              <span class="tech-tag">Vue 3</span>
              <span class="tech-tag">Vue 2</span>
              <span class="tech-tag">Nuxt</span>
              <span class="tech-tag">TypeScript</span>
              <span class="tech-tag">Pinia</span>
              <span class="tech-tag">Vite</span>
              <span class="tech-tag">Tanstack Query</span>
              <span class="tech-tag">Playwright</span>
              <span class="tech-tag">Nx</span>
              <span class="tech-tag">Tailwind</span>
              <span class="tech-tag">Storybook</span>
              <span class="tech-tag">GitLab CI</span>
              <span class="tech-tag">Cognito</span>
            </div>
          </div>

          <!-- Logicly -->
          <div class="exp-item">
            <div class="exp-header">
              <span class="exp-role">Senior Full Stack Developer</span>
              <span class="exp-date">Dec 2010 - Jan 2021</span>
            </div>
            <div class="exp-company">Logicly</div>
            <div class="exp-tech">
              <span class="tech-tag">Vue 2</span>
              <span class="tech-tag">AngularJS</span>
              <span class="tech-tag">Ruby</span>
              <span class="tech-tag">Python</span>
              <span class="tech-tag">Perl</span>
              <span class="tech-tag">Docker</span>
              <span class="tech-tag">Postgres</span>
              <span class="tech-tag">MySQL</span>
              <span class="tech-tag">DynamoDB</span>
              <span class="tech-tag">S3</span>
              <span class="tech-tag">OpenAPI</span>
            </div>
          </div>
        </div>
      </section>
    </main>


    <!-- Floating Ko-Fi Support Button -->
    <div v-if="showKofi" class="kofi-floating">
      <a :href="kofiProfileUrl" target="_blank" rel="noopener noreferrer" class="kofi-btn">
        <!-- Coffee Cup Stroke SVG Icon -->
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
          <path d="M18 8h1a4 4 0 0 1 0 8h-1" />
          <path d="M2 8h16v9a4 4 0 0 1-4 4H6a4 4 0 0 1-4-4V8z" />
          <line x1="6" y1="1" x2="6" y2="4" />
          <line x1="10" y1="1" x2="10" y2="4" />
          <line x1="14" y1="1" x2="14" y2="4" />
        </svg>
        <span>Support me on Ko-fi</span>
      </a>
    </div>
  </div>
</template>

<style>
/* Custom letter tiles transition styling if needed */
.sim-tile {
  cursor: pointer;
}
</style>
