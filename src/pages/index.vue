<script setup lang="ts">
defineOptions({
  name: 'IndexPage',
})
const user = useUserStore()
const name = ref(user.savedName)

const router = useRouter()
function go() {
  if (name.value)
    router.push(`/hi/${encodeURIComponent(name.value)}`)
}

const { t } = useI18n()
useHead({
  title: () => t('button.home'),
})

const features = computed(() => [
  { icon: 'i-carbon-flash', title: t('landing.feature1.title'), desc: t('landing.feature1.desc') },
  { icon: 'i-carbon-color-palette', title: t('landing.feature2.title'), desc: t('landing.feature2.desc') },
  { icon: 'i-carbon-language', title: t('landing.feature3.title'), desc: t('landing.feature3.desc') },
])
</script>

<template>
  <div class="landing">
    <div class="glow" aria-hidden="true" />
    <div class="glow-2" aria-hidden="true" />

    <section class="intro">
      <p class="eyebrow">
        <span class="eyebrow-icon i-carbon-campsite" />
        {{ t('landing.badge') }}
      </p>
      <h1 class="headline">
        {{ t('landing.headline') }}
      </h1>
      <p class="lead">
        {{ t('intro.desc') }}
      </p>
    </section>

    <section class="panel">
      <form class="panel-form" @submit.prevent="go">
        <label class="panel-label" for="input">{{ t('intro.whats-your-name') }}</label>
        <div class="panel-row">
          <TheInput
            v-model="name"
            :placeholder="t('intro.whats-your-name')"
            autocomplete="false"
            class="panel-input"
          />
          <button type="submit" class="panel-cta btn" :disabled="!name">
            {{ t('button.go') }}
          </button>
        </div>
        <p class="panel-hint">
          {{ t('landing.hint') }}
        </p>
      </form>
    </section>

    <ol class="steps">
      <li v-for="(feature, i) in features" :key="feature.title" class="step">
        <div class="step-top">
          <span class="step-num">0{{ i + 1 }}</span>
        </div>
        <span class="step-icon" :class="feature.icon" />
        <h3>{{ feature.title }}</h3>
        <p>{{ feature.desc }}</p>
      </li>
    </ol>
  </div>
</template>

<style scoped>
.landing {
  position: relative;
  width: 100%;
  margin: 0 auto;
  padding: 1rem clamp(1.5rem, 8vw, 6rem) 2rem;
  text-align: left;
  isolation: isolate;
  overflow-x: clip;
}

.glow,
.glow-2 {
  position: absolute;
  z-index: -1;
  border-radius: 50%;
  pointer-events: none;
  filter: blur(60px);
}

.glow {
  top: -160px;
  right: -140px;
  width: 480px;
  height: 480px;
  background: radial-gradient(closest-side, rgba(20, 184, 166, 0.35), transparent);
}

.glow-2 {
  bottom: -120px;
  left: -120px;
  width: 360px;
  height: 360px;
  background: radial-gradient(closest-side, rgba(96, 165, 250, 0.28), transparent);
}

.intro {
  max-width: 100%;
  padding-top: 2rem;
}

.eyebrow {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  margin: 0;
  padding: 0.35rem 0.85rem 0.35rem 0.5rem;
  border-radius: 999px;
  font-size: 0.75rem;
  font-weight: 500;
  letter-spacing: 0.04em;
  color: rgb(15, 118, 110);
  background: rgba(20, 184, 166, 0.12);
  box-shadow: inset 0 0 0 1px rgba(20, 184, 166, 0.25);
}

html.dark .eyebrow {
  color: rgb(153, 246, 228);
  background: rgba(45, 212, 191, 0.1);
}

.eyebrow-icon {
  display: inline-grid;
  place-items: center;
  width: 1.4rem;
  height: 1.4rem;
  border-radius: 50%;
  background: rgb(13, 148, 136);
  color: white;
  font-size: 0.8rem;
  animation: icon-spin 6s linear infinite;
}

.headline {
  margin: 1.25rem 0 0;
  font-family: 'DM Serif Display', serif;
  font-size: clamp(2.8rem, 7.5vw, 5rem);
  font-weight: 400;
  line-height: 0.98;
  letter-spacing: -0.035em;
  background: linear-gradient(120deg, #0f766e 0%, #0d9488 35%, #2563eb 100%);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}

html.dark .headline {
  background: linear-gradient(120deg, #ccfbf1 0%, #5eead4 40%, #93c5fd 100%);
  -webkit-background-clip: text;
  background-clip: text;
}

.lead {
  margin: 1.5rem 0 0;
  max-width: 48ch;
  font-size: 1.15rem;
  line-height: 1.65;
  opacity: 0.72;
}

.panel {
  position: relative;
  margin-top: 2.75rem;
  padding: 1.5rem;
  max-width: 100%;
  border-radius: 1.5rem;
  background: rgba(255, 255, 255, 0.7);
  box-shadow:
    0 1px 0 rgba(255, 255, 255, 0.8) inset,
    0 24px 60px -24px rgba(15, 118, 110, 0.35),
    0 0 0 1px rgba(128, 128, 128, 0.14);
  backdrop-filter: blur(14px);
}

html.dark .panel {
  background: rgba(20, 20, 20, 0.6);
  box-shadow:
    0 1px 0 rgba(255, 255, 255, 0.04) inset,
    0 24px 60px -24px rgba(0, 0, 0, 0.7),
    0 0 0 1px rgba(255, 255, 255, 0.07);
}

.panel-label {
  display: block;
  font-size: 0.95rem;
  font-weight: 600;
  letter-spacing: -0.01em;
}

.panel-row {
  display: flex;
  gap: 0.5rem;
  margin-top: 0.85rem;
  padding: 0.35rem;
  border-radius: 999px;
  background: rgba(128, 128, 128, 0.08);
  box-shadow: inset 0 0 0 1px rgba(128, 128, 128, 0.15);
  transition:
    box-shadow 200ms ease,
    background 200ms ease;
}

.panel-row:focus-within {
  background: rgba(20, 184, 166, 0.06);
  box-shadow: inset 0 0 0 1.5px rgba(13, 148, 136, 0.6);
}

.panel-input {
  flex: 1;
  width: auto !important;
  min-width: 0;
  padding: 0.6rem 1rem !important;
  border: none !important;
  text-align: left !important;
  font-size: 1rem;
}

.panel-cta {
  padding: 0.6rem 1.6rem !important;
  border-radius: 999px !important;
  font-weight: 600;
  letter-spacing: 0.02em;
  box-shadow: 0 8px 20px -8px rgba(13, 148, 136, 0.7);
  transition:
    transform 150ms ease,
    box-shadow 150ms ease;
}

.panel-cta:not(:disabled):hover {
  transform: translateY(-1px);
  box-shadow: 0 12px 24px -8px rgba(13, 148, 136, 0.8);
}

.panel-hint {
  margin: 0.85rem 0 0 0.25rem;
  font-size: 0.8rem;
  opacity: 0.55;
}

.steps {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 1rem;
  margin: 3.5rem 0 0;
  padding: 0;
  list-style: none;
}

.step {
  position: relative;
  padding: 1.5rem;
  border-radius: 1.25rem;
  background: rgba(128, 128, 128, 0.05);
  box-shadow: 0 0 0 1px rgba(128, 128, 128, 0.14);
  transition:
    transform 250ms ease,
    box-shadow 250ms ease,
    background 250ms ease;
}

.step:hover {
  transform: translateY(-4px);
  background: rgba(20, 184, 166, 0.06);
  box-shadow:
    0 0 0 1px rgba(20, 184, 166, 0.35),
    0 20px 40px -24px rgba(13, 148, 136, 0.6);
}

.step-top {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.step-num {
  font-family: 'DM Mono', monospace;
  font-size: 0.75rem;
  opacity: 0.45;
}

.step-icon {
  display: inline-grid;
  place-items: center;
  width: 2.75rem;
  height: 2.75rem;
  margin: 1rem 0 0.9rem;
  border-radius: 0.9rem;
  font-size: 1.35rem;
  color: rgb(13, 148, 136);
  background: linear-gradient(135deg, rgba(20, 184, 166, 0.2), rgba(59, 130, 246, 0.15));
  animation: icon-spin 6s linear infinite;
}

html.dark .step-icon {
  color: rgb(94, 234, 212);
}

.step:hover .step-icon {
  animation-duration: 1.2s;
}

.step h3 {
  margin: 0 0 0.4rem;
  font-size: 1.05rem;
  font-weight: 600;
  letter-spacing: -0.01em;
}

.step p {
  margin: 0;
  font-size: 0.9rem;
  line-height: 1.6;
  opacity: 0.7;
}

.eyebrow,
.headline,
.lead,
.panel {
  animation: fade-up 0.8s cubic-bezier(0.22, 1, 0.36, 1) both;
}

.headline {
  animation-delay: 0.1s;
}

.lead {
  animation-delay: 0.2s;
}

.panel {
  animation-delay: 0.3s;
}

@keyframes fade-up {
  from {
    opacity: 0;
    transform: translateY(16px);
    filter: blur(6px);
  }
  to {
    opacity: 1;
    transform: none;
    filter: none;
  }
}

@keyframes icon-spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

@media (prefers-reduced-motion: reduce) {
  .eyebrow-icon,
  .step-icon {
    animation: none;
  }

  .eyebrow,
  .headline,
  .lead,
  .panel {
    animation: none;
  }

  .step,
  .panel-cta {
    transition: none;
  }
}
</style>

<route lang="yaml">
meta:
  layout: home
</route>
