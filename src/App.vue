<script setup lang="ts">
import { ref, computed } from 'vue'

// --- Alphabetical Game State ---
const initialLetters = ['D', 'A', 'C', 'B']
const currentLetters = ref([...initialLetters])
const selectedIndex = ref<number | null>(null)

const alphabeticalComplete = computed(() => {
  return currentLetters.value.join('') === 'ABCD'
})

const selectTile = (index: number) => {
  if (alphabeticalComplete.value) return
  if (selectedIndex.value === null) {
    selectedIndex.value = index
  } else {
    // Swap tiles
    const temp = currentLetters.value[selectedIndex.value]
    currentLetters.value[selectedIndex.value] = currentLetters.value[index]
    currentLetters.value[index] = temp
    selectedIndex.value = null
  }
}

const resetAlphabetical = () => {
  currentLetters.value = [...initialLetters]
  selectedIndex.value = null
}

// --- Calculator Game State ---
const calcValue = ref(3)
const calcTarget = 24
const calcSteps = ref(0)
const calcSuccess = computed(() => calcValue.value === calcTarget)

const applyCalcOp = (op: 'add5' | 'mul3' | 'sub2') => {
  if (calcSuccess.value) return
  if (op === 'add5') calcValue.value += 5
  else if (op === 'mul3') calcValue.value *= 3
  else if (op === 'sub2') calcValue.value -= 2
  calcSteps.value++
}

const resetCalc = () => {
  calcValue.value = 3
  calcSteps.value = 0
}

// --- Ko-fi Profile Link ---
// The user can edit this link value easily in the code.
const kofiProfileUrl = ref('https://ko-fi.com/amurf') 
const githubUrl = ref('https://github.com')
const linkedinUrl = ref('https://linkedin.com')
const contactEmail = ref('self@amrf.dev')
</script>

<template>
  <div class="container">
    <!-- Hero Header -->
    <header class="hero">
      <h1>Ash</h1>
      <p class="tagline">Senior Software Engineer</p>
      
      <div class="social-links">
        <a :href="githubUrl" target="_blank" rel="noopener noreferrer" class="btn-brutalist">
          <svg viewBox="0 0 24 24" width="16" height="16" fill="currentColor">
            <path d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.53 1.032 1.53 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0022 12.017C22 6.484 17.522 2 12 2z"/>
          </svg>
          GitHub
        </a>
        <a :href="linkedinUrl" target="_blank" rel="noopener noreferrer" class="btn-brutalist">
          <svg viewBox="0 0 24 24" width="16" height="16" fill="currentColor">
            <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
          </svg>
          LinkedIn
        </a>
        <a :href="'mailto:' + contactEmail" class="btn-brutalist">
          <svg viewBox="0 0 24 24" width="16" height="16" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
            <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/>
            <polyline points="22,6 12,13 2,6"/>
          </svg>
          Email
        </a>
      </div>
    </header>

    <!-- Projects Showcase -->
    <section id="projects">
      <h2>projects</h2>
      <div class="apps-grid">
        <!-- Project 1: Alphabetical -->
        <div class="app-card">
          <div class="app-badge">iOS & Android App (Upcoming)</div>
          <h3 class="app-title">Alphabetical</h3>
          
          <!-- CSS Simulator -->
          <div class="app-simulator">
            <div class="sim-alphabetical">
              <div 
                v-for="(letter, index) in currentLetters" 
                :key="index"
                class="sim-tile"
                :class="{ 
                  'active': selectedIndex === index || alphabeticalComplete
                }"
                @click="selectTile(index)"
              >
                {{ letter }}
              </div>
            </div>
            
            <!-- Success Overlay inside simulator -->
            <div v-if="alphabeticalComplete" class="sim-success-overlay">
              <span class="sim-success-title">alphabetical complete</span>
              <button 
                class="btn-brutalist" 
                style="padding: 6px 14px; font-size: 0.75rem;" 
                @click="resetAlphabetical"
              >
                Play Again
              </button>
            </div>
          </div>
          
          <p class="app-description">
            A fast-paced verbal word puzzle and ordering game designed to test cognitive agility and alphabetical reflexes. Solve grids, race the timer, and compete globally.
          </p>
          <div style="display: flex; gap: 8px; font-family: var(--font-sans); font-size: 0.8rem; color: var(--text-secondary);">
            <span>• Vue</span>
            <span>• Capacitor</span>
            <span>• TypeScript</span>
          </div>
        </div>

        <!-- Project 2: Calculator Game -->
        <div class="app-card">
          <div class="app-badge">iOS & Android App (Upcoming)</div>
          <h3 class="app-title">Calculator Game</h3>
          
          <!-- CSS Simulator -->
          <div class="app-simulator">
            <div class="sim-calculator">
              <div class="sim-calc-screen">
                <div class="sim-calc-target">TARGET: {{ calcTarget }} (Steps: {{ calcSteps }})</div>
                <div class="sim-calc-value">{{ calcValue }}</div>
              </div>
              <div class="sim-calc-grid">
                <button class="sim-calc-btn accent" @click="applyCalcOp('add5')">+5</button>
                <button class="sim-calc-btn accent" @click="applyCalcOp('mul3')">×3</button>
                <button class="sim-calc-btn accent" @click="applyCalcOp('sub2')">-2</button>
              </div>
            </div>
            
            <!-- Success Overlay inside simulator -->
            <div v-if="calcSuccess" class="sim-success-overlay">
              <span class="sim-success-title">target reached</span>
              <span style="font-family: var(--font-sans); font-size: 0.75rem; color: var(--text-secondary); margin-bottom: 12px;">solved in {{ calcSteps }} steps</span>
              <button 
                class="btn-brutalist" 
                style="padding: 6px 14px; font-size: 0.75rem;" 
                @click="resetCalc"
              >
                Play Again
              </button>
            </div>
          </div>
          
          <p class="app-description">
            A minimalistic mathematical logic puzzle. Use a limited set of calculator operators to manipulate the starting value and hit the target number. Simple rules, deep strategies.
          </p>
          <div style="display: flex; gap: 8px; font-family: var(--font-sans); font-size: 0.8rem; color: var(--text-secondary);">
            <span>• Vue</span>
            <span>• Capacitor</span>
            <span>• TypeScript</span>
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
            <span class="tech-tag">AWS Serverless</span>
            <span class="tech-tag">Lambda</span>
            <span class="tech-tag">DynamoDB</span>
            <span class="tech-tag">Redshift</span>
            <span class="tech-tag">OpenSearch</span>
            <span class="tech-tag">Vue</span>
            <span class="tech-tag">TypeScript</span>
            <span class="tech-tag">React</span>
            <span class="tech-tag">Remix</span>
            <span class="tech-tag">Terraform</span>
            <span class="tech-tag">D3</span>
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
            <span class="tech-tag">Vue</span>
            <span class="tech-tag">Nuxt</span>
            <span class="tech-tag">TypeScript</span>
            <span class="tech-tag">Pinia</span>
            <span class="tech-tag">Vite</span>
            <span class="tech-tag">Tanstack Query</span>
            <span class="tech-tag">Playwright</span>
            <span class="tech-tag">NX Monorepo</span>
            <span class="tech-tag">Tailwind</span>
            <span class="tech-tag">Storybook</span>
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
            <span class="tech-tag">Vue</span>
            <span class="tech-tag">AngularJS</span>
            <span class="tech-tag">Ruby</span>
            <span class="tech-tag">Python</span>
            <span class="tech-tag">Perl</span>
            <span class="tech-tag">Docker</span>
            <span class="tech-tag">Postgres</span>
            <span class="tech-tag">MySQL</span>
            <span class="tech-tag">DynamoDB</span>
            <span class="tech-tag">AWS S3</span>
            <span class="tech-tag">OpenAPI</span>
          </div>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer>
      <p>© {{ new Date().getFullYear() }} Ash. Built with Vue, Vite & pure CSS.</p>
    </footer>

    <!-- Floating Ko-Fi Support Button -->
    <div class="kofi-floating">
      <a :href="kofiProfileUrl" target="_blank" rel="noopener noreferrer" class="kofi-btn">
        <!-- Coffee Cup SVG Icon -->
        <svg viewBox="0 0 24 24">
          <path d="M2 21h18v-2H2v2zM20 8h-2V5h2v3zm2-5h-4v5h4V3zM4 19h12v-4H4v4zm0-6h12v-4H4v4zm0-6h12V3H4v4z"/>
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
