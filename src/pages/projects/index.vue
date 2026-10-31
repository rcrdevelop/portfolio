<template>
  <q-page>
    <PageHeader
      label="Portafolio"
      title="Proyectos"
      subtitle="Interfaces interactivas de proyectos reales desarrollados a lo largo de 6+ años"
      image="/images/hero/projects-hero.webp"
    />

    <div class="container q-py-xl">
      <!-- Filtros -->
      <q-card flat class="q-mb-xl bento-card">
        <q-card-section>
          <div class="text-h6 text-weight-bold q-mb-md">
            <q-icon name="apps" color="primary" class="q-mr-sm" />
            Seleccionar Proyecto Interactivo
          </div>
          <div class="row q-gutter-sm">
            <q-chip
              v-for="project in projects"
              :key="project.id"
              clickable
              :icon="project.icon"
              class="project-filter-chip"
              :color="selectedProject?.id === project.id ? 'primary' : 'grey-2'"
              :text-color="
                selectedProject?.id === project.id ? 'white' : 'grey-9'
              "
              @click="selectProject(project)"
              :label="project.name"
            />
          </div>
        </q-card-section>
      </q-card>

      <!-- Visualización de Interface -->
      <transition name="project-switch" mode="out-in">
        <div v-if="selectedProject" :key="selectedProject.id">
          <q-card flat class="q-mb-md browser-frame">
            <q-card-section class="bg-dark text-white q-py-sm">
              <div class="row items-center">
                <div class="row items-center q-gutter-xs q-mr-md">
                  <span class="window-dot dot-red"></span>
                  <span class="window-dot dot-yellow"></span>
                  <span class="window-dot dot-green"></span>
                </div>
                <div class="col">
                  <div class="text-subtitle1 text-weight-bold">
                    {{ selectedProject.name }}
                  </div>
                  <div class="text-caption text-grey-4">
                    {{ selectedProject.stack }}
                  </div>
                </div>
                <div class="col-auto row items-center q-gutter-sm">
                  <q-btn
                    flat
                    round
                    dense
                    icon="open_in_new"
                    color="grey-4"
                    :href="selectedProject.url"
                    target="_blank"
                    :aria-label="'Abrir ' + selectedProject.name"
                  />
                  <q-badge
                    color="accent"
                    class="q-px-sm q-py-xs text-weight-bold"
                    :label="selectedProject.category"
                  />
                </div>
              </div>
            </q-card-section>
          </q-card>

          <!-- Captura del sitio desplegado -->
          <q-card flat class="browser-frame overflow-hidden">
            <a
              :href="selectedProject.url"
              target="_blank"
              rel="noopener"
              :aria-label="'Abrir ' + selectedProject.name"
            >
              <q-img
                :key="selectedProject.id"
                :src="selectedProject.shot"
                :alt="'Demo de ' + selectedProject.name"
                class="app-shot"
              />
            </a>
            <q-card-actions align="center" class="q-pa-md q-gutter-sm">
              <q-btn
                color="primary"
                unelevated
                no-caps
                icon-right="open_in_new"
                :label="'Visitar ' + selectedProject.name"
                :href="selectedProject.url"
                target="_blank"
              />
              <q-btn
                color="grey-8"
                outline
                unelevated
                no-caps
                icon="code"
                icon-right="open_in_new"
                label="Ver código"
                :href="selectedProject.repo"
                target="_blank"
              />
            </q-card-actions>
          </q-card>

          <!-- Información del Proyecto -->
          <q-card flat class="q-mt-xl bento-card">
            <q-card-section>
              <div class="text-h6 text-weight-bold q-mb-md">
                Sobre este Proyecto
              </div>
              <p class="text-body1 q-mb-md">
                {{ selectedProject.description }}
              </p>

              <div class="row q-col-gutter-md">
                <div class="col-12 col-md-6">
                  <div class="text-subtitle1 text-weight-bold q-mb-sm">
                    Stack Tecnológico:
                  </div>
                  <p class="text-body2 text-grey-8">
                    {{ selectedProject.stack }}
                  </p>
                </div>
                <div class="col-12 col-md-6">
                  <div class="text-subtitle1 text-weight-bold q-mb-sm">
                    Características:
                  </div>
                  <div class="q-gutter-xs">
                    <q-chip
                      v-for="feature in selectedProject.features"
                      :key="feature"
                      :label="feature"
                      color="secondary"
                      text-color="white"
                      size="sm"
                    />
                  </div>
                </div>
              </div>
            </q-card-section>
          </q-card>
        </div>

        <!-- Mensaje inicial -->
        <div v-else class="text-center q-py-xl">
          <q-icon name="touch_app" size="100px" color="grey-5" />
          <div class="text-h6 text-grey-7 q-mt-md">
            Selecciona un proyecto para ver su interfaz
          </div>
        </div>
      </transition>
    </div>
  </q-page>
</template>

<script setup lang="ts">
import PageHeader from "@/components/PageHeader.vue";
import { usePageMeta } from "@/composables/seo";
import { ref } from "vue";

usePageMeta(
  "Proyectos",
  "Proyectos reales desplegados por Ricardo Contreras: dashboards, e-commerce headless, telefonía, reservas y apps móviles sobre Firebase.",
  "/projects"
);

const projects = [
  {
    id: 1,
    icon: "casino",
    name: "Plataforma HUD Poker",
    category: "Dashboard",
    stack: "C# .NET + MongoDB",
    description:
      "Dashboard en tiempo real para análisis de juego de poker con estadísticas avanzadas y reproductor de manos.",
    features: ["Real-time", "Analytics", "Data Visualization", "Desktop App"],
    url: "https://poker-hud.rcrdevelop.dev",
    repo: "https://github.com/rcrdevelop/rcr-poker-hud",
    shot: "/images/projects/live-hud.webp"
  },
  {
    id: 2,
    icon: "apartment",
    name: "Sistema Inmobiliario",
    category: "Dashboard",
    stack: "PHP + MariaDB + DocuSign",
    description:
      "Plataforma para gestión de propiedades con firma digital de contratos integrada.",
    features: ["CRUD", "DocuSign", "PDF Generation", "Email Automation"],
    url: "https://real-state.rcrdevelop.dev",
    repo: "https://github.com/rcrdevelop/rcr-real-estate",
    shot: "/images/projects/live-real-estate.webp"
  },
  {
    id: 3,
    icon: "shopping_bag",
    name: "Tienda Shopify",
    category: "Ecommerce",
    stack: "Shopify Liquid + Dawn Theme",
    description:
      "Tema personalizado para tienda online con carrito optimizado y checkout mejorado.",
    features: [
      "Responsive",
      "Fast Checkout",
      "Product Filters",
      "SEO Optimized"
    ],
    url: "https://headless.rcrdevelop.dev",
    repo: "https://github.com/rcrdevelop/rcr-shopify-headless",
    shot: "/images/projects/live-headless.webp"
  },
  {
    id: 4,
    icon: "phone_in_talk",
    name: "Plataforma de Telefonía",
    category: "Dashboard",
    stack: "Angular + Spring Boot + MariaDB",
    description:
      "Sistema completo de números temporales con integración de múltiples pasarelas de pago.",
    features: [
      "Multi-payment",
      "SMS Integration",
      "User Management",
      "Billing"
    ],
    url: "https://phones.rcrdevelop.dev",
    repo: "https://github.com/rcrdevelop/rcr-telephony",
    shot: "/images/projects/live-phone.webp"
  },
  {
    id: 5,
    icon: "mood",
    name: "App Migo - Niños",
    category: "Web App",
    stack: "Vue.js + Vuetify + Node.js + MongoDB",
    description:
      "Aplicación web interactiva para que niños expresen sus emociones a través de juegos.",
    features: [
      "Interactive UI",
      "Gamification",
      "Progress Tracking",
      "Responsive"
    ],
    url: "https://migo.rcrdevelop.dev",
    repo: "https://github.com/rcrdevelop/rcr-migo-kids",
    shot: "/images/projects/live-migo.webp"
  },
  {
    id: 6,
    icon: "flight_takeoff",
    name: "Sistema de Aerolínea",
    category: "Dashboard",
    stack: "React + Node.js + MongoDB",
    description:
      "Plataforma de búsqueda y reserva de vuelos con sistema de paginación avanzado.",
    features: ["Flight Search", "Booking System", "Pagination", "Filters"],
    url: "https://sky-book.rcrdevelop.dev",
    repo: "https://github.com/rcrdevelop/rcr-airline-booking",
    shot: "/images/projects/live-skybook.webp"
  },
  {
    id: 7,
    icon: "smart_display",
    name: "Buscador de Videos",
    category: "Web App",
    stack: "Vue.js + Vuetify + MongoDB",
    description: "Plataforma de búsqueda con respuestas tipo YouTube.",
    features: ["Search Engine", "Video Player", "Recommendations", "Comments"],
    url: "https://videohub.rcrdevelop.dev",
    repo: "https://github.com/rcrdevelop/rcr-video-hub",
    shot: "/images/projects/live-video.webp"
  }
];

const selectedProject = ref<any>(projects[0]);

function selectProject(project: any) {
  selectedProject.value = project;
}
</script>

<style scoped>
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding-left: 20px;
  padding-right: 20px;
}

.project-filter-chip {
  font-weight: 600;
  padding: 10px 14px;
  transition:
    transform 0.24s cubic-bezier(0.22, 1, 0.36, 1),
    box-shadow 0.24s ease;
}

.project-filter-chip:hover {
  transform: translateY(-3px);
  box-shadow: 0 8px 18px color-mix(in srgb, var(--q-primary) 22%, transparent);
}

.window-dot {
  width: 11px;
  height: 11px;
  border-radius: 50%;
  display: inline-block;
}

.dot-red {
  background: #ef4444;
}

.dot-yellow {
  background: #f59e0b;
}

.dot-green {
  background: #10b981;
}

.app-shot {
  display: block;
  width: 100%;
  border-radius: 0;
  background: #fff;
  transition: opacity 0.2s ease;
}

.app-shot:hover {
  opacity: 0.9;
}
</style>
