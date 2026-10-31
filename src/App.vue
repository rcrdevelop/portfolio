<template>
  <q-layout view="hHh lpR lFf">
    <!-- Header -->
    <q-header class="app-header">
      <q-toolbar class="app-toolbar">
        <q-toolbar-title class="text-weight-bold brand">
          <q-icon name="terminal" size="sm" class="q-mr-sm brand-icon" />
          {{ SITE.brand }}
        </q-toolbar-title>

        <!-- Navegación Desktop -->
        <div class="gt-sm q-gutter-md row items-center">
          <q-btn flat label="Inicio" to="/" class="nav-btn" />
          <q-btn flat label="Sobre Mí" to="/about" class="nav-btn" />
          <q-btn flat label="Skills" to="/skills" class="nav-btn" />
          <q-btn flat label="Proyectos" to="/projects" class="nav-btn" />
          <q-btn
            outline
            size="sm"
            color="accent"
            label="Contacto"
            to="/contact"
            class="q-px-md"
          />
        </div>

        <!-- Menú Mobile -->
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Abrir menú"
          class="lt-md"
          @click="mobileMenu = true"
        />
      </q-toolbar>
    </q-header>

    <!-- Menú Mobile (Dialog) -->
    <q-dialog v-model="mobileMenu" position="right" full-height>
      <q-card dark style="width: 300px">
        <q-card-section>
          <div class="text-h6">Menú</div>
        </q-card-section>

        <q-list dark>
          <q-item clickable v-ripple to="/" @click="mobileMenu = false">
            <q-item-section avatar>
              <q-icon name="home" />
            </q-item-section>
            <q-item-section>Inicio</q-item-section>
          </q-item>

          <q-item clickable v-ripple to="/about" @click="mobileMenu = false">
            <q-item-section avatar>
              <q-icon name="person" />
            </q-item-section>
            <q-item-section>Sobre Mí</q-item-section>
          </q-item>

          <q-item clickable v-ripple to="/skills" @click="mobileMenu = false">
            <q-item-section avatar>
              <q-icon name="build" />
            </q-item-section>
            <q-item-section>Skills</q-item-section>
          </q-item>

          <q-item clickable v-ripple to="/projects" @click="mobileMenu = false">
            <q-item-section avatar>
              <q-icon name="folder" />
            </q-item-section>
            <q-item-section>Proyectos</q-item-section>
          </q-item>

          <q-item clickable v-ripple to="/contact" @click="mobileMenu = false">
            <q-item-section avatar>
              <q-icon name="email" />
            </q-item-section>
            <q-item-section>Contacto</q-item-section>
          </q-item>
        </q-list>
      </q-card>
    </q-dialog>

    <!-- Page Container -->
    <q-page-container>
      <router-view v-slot="{ Component }">
        <transition name="page-fade" mode="out-in">
          <component :is="Component" />
        </transition>
      </router-view>
    </q-page-container>

    <!-- Footer slim -->
    <footer class="app-footer">
      <div class="app-footer__inner">
        <div class="footer-copy">
          © 2026 {{ SITE.brand }} · Hecho con Quasar + Firebase
        </div>
        <div class="footer-social">
          <q-btn
            flat
            round
            dense
            icon="code"
            :href="SITE.social.github"
            target="_blank"
            aria-label="GitHub"
          />
          <q-btn
            flat
            round
            dense
            icon="work"
            :href="SITE.social.linkedin"
            target="_blank"
            aria-label="LinkedIn"
          />
          <q-btn
            flat
            round
            dense
            icon="mail"
            :href="`mailto:${SITE.email}`"
            aria-label="Email"
          />
        </div>
      </div>
    </footer>
  </q-layout>
</template>

<script setup lang="ts">
import { ref } from "vue";
import { SITE } from "@/config/site";

const mobileMenu = ref(false);
</script>

<style scoped>
.app-header {
  background: rgba(10, 10, 10, 0.8);
  backdrop-filter: blur(10px);
  border-bottom: 1px solid var(--bento-border);
}

.app-toolbar {
  min-height: 56px;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 16px;
}

.brand {
  font-size: 1.05rem;
  letter-spacing: -0.01em;
}

.brand-icon {
  color: var(--q-accent);
}

.nav-btn {
  position: relative;
  font-weight: 600;
  color: var(--bento-muted);
  transition:
    color 0.22s ease,
    transform 0.22s ease;
}

.nav-btn::after {
  content: "";
  position: absolute;
  bottom: 4px;
  left: 16px;
  right: 16px;
  height: 2px;
  border-radius: 999px;
  background: var(--q-accent);
  transform: scaleX(0);
  transition: transform 0.25s cubic-bezier(0.22, 1, 0.36, 1);
}

.nav-btn:hover {
  color: var(--bento-text);
}

.nav-btn:hover::after,
.nav-btn.q-router-link--active::after {
  transform: scaleX(1);
}

.nav-btn.q-router-link--active {
  color: var(--bento-text);
}

.app-footer {
  border-top: 1px solid var(--bento-border);
  margin-top: 24px;
}

.app-footer__inner {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px 16px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
  flex-wrap: wrap;
}

.footer-copy {
  color: var(--bento-muted);
  font-size: 0.8rem;
}

.footer-social :deep(.q-btn) {
  color: var(--bento-muted);
}

.footer-social :deep(.q-btn:hover) {
  color: var(--q-accent);
}
</style>
