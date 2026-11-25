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
    <section class="hero">
      <div class="hero-badge">
        <span i-carbon-campsite inline-block />
        {{ t('landing.badge') }}
      </div>

      <h1 class="hero-title">
        {{ t('landing.headline') }}
      </h1>
      <p class="hero-subtitle">
        {{ t('intro.desc') }}
      </p>

      <form class="hero-form" @submit.prevent="go">
        <TheInput
          v-model="name"
          :placeholder="t('intro.whats-your-name')"
          autocomplete="false"
          class="hero-input"
        />
        <label class="hidden" for="input">{{ t('intro.whats-your-name') }}</label>
        <button
          type="submit"
          class="hero-cta btn"
          :disabled="!name"
        >
          {{ t('button.go') }}
          <span i-carbon-arrow-right ml-1 inline-block align-middle />
        </button>
      </form>
      <p class="hero-hint">
        {{ t('landing.hint') }}
      </p>
    </section>

    <section class="features">
      <article
        v-for="feature in features"
        :key="feature.title"
        class="feature-card"
      >
        <div class="feature-icon">
          <span :class="feature.icon" />
        </div>
        <h3>{{ feature.title }}</h3>
        <p>{{ feature.desc }}</p>
      </article>
    </section>
  </div>
</template>

<style scoped>
.landing {
  max-width: 960px;
  margin: 0 auto;
}

.hero {
  padding: 3rem 1rem 4rem;
  border-radius: 1.5rem;
  background:
    radial-gradient(circle at 15% 0%, rgba(13, 148, 136, 0.18), transparent 45%),
    radial-gradient(circle at 85% 100%, rgba(59, 130, 246, 0.12), transparent 45%);
}

html.dark .hero {
  background:
    radial-gradient(circle at 15% 0%, rgba(45, 212, 191, 0.14), transparent 45%),
    radial-gradient(circle at 85% 100%, rgba(96, 165, 250, 0.1), transparent 45%);
}

.hero-badge {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  padding: 0.3rem 0.8rem;
  border-radius: 999px;
  font-size: 0.8rem;
  color: rgb(15, 118, 110);
  background: rgba(13, 148, 136, 0.1);
}

html.dark .hero-badge {
  color: rgb(94, 234, 212);
}

.hero-title {
  margin: 1.25rem auto 0;
  max-width: 14ch;
  font-family: 'DM Serif Display', serif;
  font-size: clamp(2.5rem, 6vw, 4rem);
  line-height: 1.05;
  letter-spacing: -0.02em;
  background: linear-gradient(135deg, #0f766e 0%, #2563eb 100%);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}

html.dark .hero-title {
  background: linear-gradient(135deg, #5eead4 0%, #93c5fd 100%);
  -webkit-background-clip: text;
  background-clip: text;
}

.hero-subtitle {
  margin: 1rem auto 0;
  max-width: 52ch;
  font-size: 1.1rem;
  line-height: 1.6;
  opacity: 0.8;
}

.hero-form {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  gap: 0.75rem;
  margin-top: 2rem;
}

.hero-input {
  width: 260px !important;
  padding: 0.6rem 1rem !important;
  border-radius: 999px !important;
  text-align: left !important;
}

.hero-cta {
  padding: 0.6rem 1.5rem !important;
  border-radius: 999px !important;
  font-size: 0.95rem;
}

.hero-hint {
  margin-top: 0.9rem;
  font-size: 0.8rem;
  opacity: 0.55;
}

.features {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(230px, 1fr));
  gap: 1.25rem;
  margin-top: 2.5rem;
}

.feature-card {
  padding: 1.5rem;
  text-align: left;
  border-radius: 1rem;
  border: 1px solid rgba(128, 128, 128, 0.2);
  transition:
    transform 200ms ease,
    box-shadow 200ms ease;
}

.feature-card:hover {
  transform: translateY(-3px);
  box-shadow: 0 10px 30px -15px rgba(13, 148, 136, 0.45);
}

.feature-icon {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 2.5rem;
  height: 2.5rem;
  margin-bottom: 1rem;
  border-radius: 0.75rem;
  font-size: 1.25rem;
  color: rgb(15, 118, 110);
  background: rgba(13, 148, 136, 0.12);
}

html.dark .feature-icon {
  color: rgb(94, 234, 212);
}

.feature-icon > span,
.hero-badge > span {
  display: inline-block;
  animation: icon-spin 6s linear infinite;
}

.feature-card:hover .feature-icon > span {
  animation-duration: 1.2s;
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
  .feature-icon > span,
  .hero-badge > span {
    animation: none;
  }
}

.feature-card h3 {
  margin: 0 0 0.4rem;
  font-size: 1.05rem;
  font-weight: 600;
}

.feature-card p {
  margin: 0;
  font-size: 0.9rem;
  line-height: 1.55;
  opacity: 0.7;
}
</style>

<route lang="yaml">
meta:
  layout: home
</route>
