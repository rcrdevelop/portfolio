<template>
  <q-page>
    <main class="bento-grid">
      <!-- 1. Intro -->
      <section
        class="bento-card bento-card--pad intro-card animate-fade-up"
        style="--i: 0"
      >
        <div class="bento-card-bg">
          <img
            src="/images/hero/home-hero.webp"
            alt=""
            aria-hidden="true"
            fetchpriority="high"
          />
        </div>
        <div class="intro-content">
          <div class="bento-label">Bienvenido</div>
          <h1 class="intro-title text-weight-bold">
            Hola, soy Ricardo Contreras, desarrollador fullstack freelance con
            6+ años de experiencia.
          </h1>
          <p class="intro-text">
            He evolucionado desde aplicaciones desktop en C# .NET hasta
            arquitecturas complejas que integran plataformas de telefonía,
            pasarelas de pago y servicios en la nube.
          </p>
          <p class="intro-text">
            Mi enfoque combina solidez técnica con comprensión de negocio:
            construyo productos que resuelven problemas reales.
          </p>
          <div class="intro-actions">
            <a
              class="bento-btn"
              :href="SITE.social.github"
              target="_blank"
              rel="noopener"
              aria-label="GitHub"
            >
              <q-icon name="code" size="20px" />
            </a>
            <a
              class="bento-btn"
              :href="SITE.social.linkedin"
              target="_blank"
              rel="noopener"
              aria-label="LinkedIn"
            >
              <q-icon name="work" size="20px" />
            </a>
            <a
              class="bento-btn"
              :href="`mailto:${SITE.email}`"
              aria-label="Email"
            >
              <q-icon name="mail" size="20px" />
            </a>
            <q-btn
              unelevated
              color="primary"
              label="Ver Proyectos"
              to="/projects"
              icon-right="arrow_forward"
              class="q-ml-sm"
            />
          </div>
        </div>
      </section>

      <!-- 2. Stack & herramientas -->
      <section
        class="bento-card bento-card--pad stack-card animate-fade-up"
        style="--i: 1"
      >
        <h2 class="text-h6 text-weight-bold q-mt-none q-mb-md">
          Stack &amp; herramientas
        </h2>
        <div
          v-for="group in stackGroups"
          :key="group.label"
          class="stack-group q-mb-md"
        >
          <div class="bento-label q-mb-xs">{{ group.label }}</div>
          <div class="stack-chips">
            <span v-for="item in group.items" :key="item" class="bento-chip">{{
              item
            }}</span>
          </div>
        </div>
      </section>

      <!-- 3. Contacto -->
      <section
        class="bento-card bento-card--pad contact-card animate-fade-up"
        style="--i: 2"
      >
        <h2 class="text-h6 text-weight-bold q-mt-none q-mb-md">
          ¡Trabajemos juntos!
        </h2>
        <div class="bento-label q-mb-xs">Contacto</div>
        <a :href="`mailto:${SITE.email}`" class="contact-link">{{
          SITE.email
        }}</a>
        <div class="contact-meta">{{ SITE.location.city }} · Remote</div>

        <div class="bento-label q-mt-lg q-mb-xs">Encuéntrame en</div>
        <div class="column q-gutter-xs">
          <a
            :href="SITE.social.linkedin"
            target="_blank"
            rel="noopener"
            class="contact-link"
            >LinkedIn <q-icon name="north_east" size="12px"
          /></a>
          <a
            :href="SITE.social.github"
            target="_blank"
            rel="noopener"
            class="contact-link"
            >GitHub <q-icon name="north_east" size="12px"
          /></a>
          <a :href="`mailto:${SITE.email}`" class="contact-link"
            >Email <q-icon name="north_east" size="12px"
          /></a>
        </div>

        <div class="q-mt-lg">
          <div class="bento-label q-mb-xs">Disponibilidad</div>
          <div class="row items-center q-gutter-sm">
            <span class="status-dot"></span>
            <span class="contact-status">Aceptando nuevos proyectos</span>
          </div>
          <div class="contact-meta"> Respuesta en menos de 24h </div>
        </div>

        <q-btn
          flat
          color="accent"
          label="Contactar"
          to="/contact"
          icon-right="arrow_forward"
          class="q-mt-lg self-start"
          no-caps
        />
      </section>

      <!-- 4. Timezone -->
      <TimeZoneCard class="animate-fade-up" style="--i: 3" />

      <!-- 5. Proyectos (link card con marquee) -->
      <router-link
        to="/projects"
        class="bento-card bento-card--link projects-card animate-fade-up"
        style="--i: 4"
      >
        <div class="marquee" aria-hidden="true">
          <div class="marquee-row marquee-row--ltr">
            <img
              v-for="img in marqueeRowA"
              :key="`a-${img}`"
              :src="img"
              alt=""
              loading="lazy"
              decoding="async"
              width="120"
              height="72"
            />
          </div>
          <div class="marquee-row marquee-row--rtl">
            <img
              v-for="img in marqueeRowB"
              :key="`b-${img}`"
              :src="img"
              alt=""
              loading="lazy"
              decoding="async"
              width="120"
              height="72"
            />
          </div>
        </div>
        <div class="projects-card__scrim"></div>
        <h2 class="text-h6 text-weight-bold projects-card__title q-ma-none">
          Proyectos
        </h2>
        <q-icon name="north_east" class="bento-arrow" />
      </router-link>

      <!-- 6. Now -->
      <section
        class="bento-card bento-card--pad now-card animate-fade-up"
        style="--i: 5"
      >
        <div class="row items-center justify-between">
          <div class="row items-center q-gutter-sm">
            <h2 class="text-h6 text-weight-bold q-ma-none">Ahora</h2>
            <a
              href="https://sive.rs/nowff"
              target="_blank"
              rel="noopener"
              class="now-what"
              >¿qué es esto?</a
            >
          </div>
          <div class="now-date"><span class="now-dot"></span>{{ nowDate }}</div>
        </div>
        <p class="now-text q-mt-md">{{ SITE.now.text }}</p>
        <router-link to="/projects" class="contact-link"
          >ver plan <q-icon name="north_east" size="12px"
        /></router-link>
      </section>

      <!-- 7. Link cards -->
      <router-link
        to="/skills"
        class="bento-card bento-card--link link-card link-card--skills animate-fade-up"
        style="--i: 7"
      >
        <h2 class="text-h6 text-weight-bold q-ma-none">Skills</h2>
        <q-icon name="north_east" class="bento-arrow" />
      </router-link>

      <router-link
        to="/about"
        class="bento-card bento-card--link link-card link-card--about animate-fade-up"
        style="--i: 8"
      >
        <h2 class="text-h6 text-weight-bold q-ma-none">Sobre mí</h2>
        <q-icon name="north_east" class="bento-arrow" />
      </router-link>

      <!-- 8. Métricas -->
      <section
        class="bento-card bento-card--pad metrics-card animate-fade-up"
        style="--i: 9"
      >
        <div class="metrics-row">
          <div v-for="metric in metrics" :key="metric.label" class="metric">
            <div class="text-h5 text-weight-bold metric-value">
              {{ metric.value }}
            </div>
            <div class="metric-label">{{ metric.label }}</div>
          </div>
        </div>
      </section>

      <!-- 9. Footer card -->
      <section
        class="bento-card bento-card--pad footer-card animate-fade-up"
        style="--i: 10"
      >
        <span class="footer-line">
          © 2026 · Hecho con
          <q-icon name="favorite" color="accent" size="14px" /> usando Quasar +
          Firebase.
        </span>
      </section>
    </main>
  </q-page>
</template>

<script setup lang="ts">
import TimeZoneCard from "@/components/TimeZoneCard.vue";
import { SITE } from "@/config/site";
import { usePageMeta } from "@/composables/seo";

usePageMeta(
  "Inicio",
  "Portafolio de Ricardo Contreras — desarrollador fullstack freelance. Proyectos reales desplegados: web, móviles y cloud con Vue, Quasar y Firebase.",
  "/"
);

const metrics = [
  { value: "10+", label: "Proyectos" },
  { value: "6+", label: "Años" },
  { value: "15+", label: "Tecnologías" },
  { value: "100%", label: "Satisfacción" }
];

const stackGroups = [
  {
    label: "Lenguajes",
    items: ["TypeScript", "JavaScript", "C#", "PHP", "Java", "SQL"]
  },
  {
    label: "Frontend",
    items: ["Vue 3", "Quasar", "Angular", "React", "Vuetify", "Liquid"]
  },
  {
    label: "Backend",
    items: ["Node.js", ".NET", "Spring Boot", "Express", "Firebase"]
  },
  { label: "Datos", items: ["MongoDB", "MariaDB", "Firestore", "MySQL"] },
  {
    label: "Cloud & herramientas",
    items: ["Firebase", "Cloud Run", "Git", "Docker", "Vite"]
  },
  {
    label: "Negocio",
    items: ["Shopify", "WordPress", "Pasarelas de pago", "SMS/Telefonía"]
  }
];

const projectThumbs = [
  "/images/projects/poker-hud.webp",
  "/images/projects/telephony.webp",
  "/images/projects/real-estate/apartamento-centrico.webp",
  "/images/projects/real-estate/casa-moderna.webp",
  "/images/projects/shopify/vestido-elegante.webp",
  "/images/projects/shopify/bolso-de-mano.webp"
];

const marqueeRowA = [...projectThumbs, ...projectThumbs];
const marqueeRowB = [...projectThumbs]
  .reverse()
  .concat(projectThumbs.slice().reverse());

const nowDate = new Intl.DateTimeFormat("es-CO", {
  day: "numeric",
  month: "short",
  year: "numeric"
}).format(new Date(SITE.now.date));
</script>

<style scoped lang="scss">
.bento-grid {
  max-width: 1200px;
  margin: 0 auto;
  padding: 16px;
  display: grid;
  grid-template-columns: 1fr;
  gap: 12px;
}

@media (min-width: 600px) {
  .bento-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (min-width: 1024px) {
  .bento-grid {
    grid-template-columns: repeat(4, 1fr);
    gap: 16px;
    padding: 24px;
  }

  .intro-card {
    grid-column: span 3;
    grid-row: span 2;
  }
  .stack-card {
    grid-column: span 1;
    grid-row: span 3;
  }
  .contact-card {
    grid-column: span 1;
    grid-row: span 2;
  }
  .metrics-card {
    grid-column: span 2;
  }
}

// Intro
.intro-card {
  min-height: 420px;
  display: flex;
  align-items: flex-end;
  overflow: hidden;
}

.intro-content {
  position: relative;
  z-index: 1;
}

.intro-title {
  font-size: 2rem;
  line-height: 1.2;
  letter-spacing: -0.02em;
  color: var(--bento-text);
  margin: 14px 0 16px;
}

.intro-text {
  color: var(--bento-muted);
  font-size: 0.95rem;
  line-height: 1.55;
  max-width: 560px;
  margin: 0 0 10px;
}

.intro-actions {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-top: 22px;
  flex-wrap: wrap;
}

@media (max-width: 599px) {
  .intro-card {
    min-height: 0;
  }
  .intro-title {
    font-size: 1.6rem;
  }
}

// Stack
.stack-chips {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
  margin-top: 6px;
}

// Contact
.contact-card {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.contact-status {
  color: var(--bento-text);
  font-size: 0.9rem;
}

.contact-link {
  color: var(--q-accent);
  text-decoration: none;
  font-size: 0.92rem;
  display: inline-flex;
  align-items: center;
  gap: 4px;
}

.contact-link:hover {
  text-decoration: underline;
}

.contact-meta {
  color: var(--bento-muted);
  font-size: 0.8rem;
  margin-top: 4px;
}

// Projects marquee card
.projects-card {
  min-height: 160px;
  display: flex;
  align-items: flex-end;
  overflow: hidden;
  text-decoration: none;
  padding: 20px;
}

.marquee {
  position: absolute;
  inset: 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 10px;
  opacity: 0.55;
  overflow: hidden;
}

.marquee-row {
  display: flex;
  gap: 10px;
  width: max-content;
  animation: marqueeScroll 40s linear infinite;
}

.marquee-row--rtl {
  animation-direction: reverse;
}

.marquee-row img {
  height: 72px;
  width: 120px;
  object-fit: cover;
  border-radius: 8px;
  border: 1px solid var(--bento-border);
}

@keyframes marqueeScroll {
  from {
    transform: translateX(0);
  }
  to {
    transform: translateX(-50%);
  }
}

@media (prefers-reduced-motion: reduce) {
  .marquee-row {
    animation: none;
  }
}

.projects-card__scrim {
  position: absolute;
  inset: 0;
  background: linear-gradient(
    180deg,
    rgba(10, 10, 10, 0.25) 0%,
    rgba(10, 10, 10, 0.85) 100%
  );
}

.projects-card__title {
  position: relative;
  z-index: 1;
  color: var(--bento-text);
}

// Now card
.now-what {
  color: var(--bento-muted);
  font-size: 0.72rem;
  text-decoration: underline;
  text-underline-offset: 2px;
}

.now-date {
  color: var(--bento-muted);
  font-size: 0.78rem;
  display: inline-flex;
  align-items: center;
  gap: 6px;
}

.now-dot {
  width: 7px;
  height: 7px;
  border-radius: 50%;
  background: var(--q-negative);
}

.now-text {
  color: var(--bento-muted);
  font-size: 0.9rem;
  line-height: 1.5;
  margin-bottom: 10px;
}

// Link cards
.link-card {
  min-height: 120px;
  display: flex;
  align-items: center;
  padding: 20px;
  text-decoration: none;
  color: var(--bento-text);
}

.link-card--skills {
  background-image: repeating-linear-gradient(
    -45deg,
    rgba(96, 165, 250, 0.12) 0 2px,
    transparent 2px 12px
  );
}

.link-card--about {
  background-image: radial-gradient(
    rgba(255, 255, 255, 0.08) 1.5px,
    transparent 1.5px
  );
  background-size: 18px 18px;
}

// Metrics
.metrics-card {
  display: flex;
  align-items: center;
}

.metrics-row {
  display: flex;
  width: 100%;
  justify-content: space-around;
  gap: 12px;
  flex-wrap: wrap;
}

.metric {
  text-align: center;
}

.metric-value {
  color: var(--q-accent);
}

.metric-label {
  color: var(--bento-muted);
  font-size: 0.78rem;
  margin-top: 2px;
}

// Footer card
.footer-card {
  text-align: center;
  color: var(--bento-muted);
  font-size: 0.78rem;
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 64px;
}

.footer-line {
  display: inline-flex;
  flex-wrap: wrap;
  gap: 4px;
  align-items: center;
  justify-content: center;
}
</style>
