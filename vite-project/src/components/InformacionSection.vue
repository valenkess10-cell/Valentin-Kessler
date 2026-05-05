<template>
  <div class="info-card">
    <!-- Navegación por pestañas -->
    <div class="info-tabs">
      <button
        v-for="tab in tabs"
        :key="tab.id"
        class="info-tab"
        :class="{ active: activeTab === tab.id }"
        @click="activeTab = tab.id"
      >
        {{ tab.label }}
      </button>
    </div>

    <!-- Contenido: Acerca de -->
    <div v-if="activeTab === 'acerca'" class="info-panel">
      <div class="info-logo-row">
        <div class="info-logo-circle">RMM</div>
        <div>
          <p class="info-app-name">Armado de Bolsas</p>
          <p class="info-app-sub">Sistema interno — Laboratorios Roemmers</p>
        </div>
      </div>
      <p class="info-desc">
        Plataforma para el armado, control y trazabilidad de bolsas de medicamentos
        por paciente. Permite registrar, auditar y confirmar el despacho con
        trazabilidad completa[cite: 6].
      </p>
      <div class="info-badges">
        <span class="badge">Uso interno</span>
        <span class="badge">Sector farmacéutico</span>
        <span class="badge">Control de calidad</span>
      </div>
    </div>

    <!-- Contenido: Versión -->
    <div v-else-if="activeTab === 'version'" class="info-panel">
      <table class="version-table">
        <tbody>
          <tr v-for="row in versionRows" :key="row.label">
            <td class="version-label">{{ row.label }}</td>
            <td class="version-value">
              <span v-if="row.isStatus" class="status-dot" />
              {{ row.value }}
            </td>
          </tr>
        </tbody>
      </table>
    </div>

    <!-- Contenido: Contacto Institucional -->
    <div v-else-if="activeTab === 'contacto'" class="info-panel">
      <div v-for="item in contactItems" :key="item.label" class="contact-row">
        <div class="contact-icon-wrap" v-html="item.icon" />
        <span class="contact-label">{{ item.label }}</span>
        <span class="contact-value">{{ item.value }}</span>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const activeTab = ref('acerca')

const tabs = [
  { id: 'acerca', label: 'Acerca de' },
  { id: 'version', label: 'Versión' },
  { id: 'contacto', label: 'Contacto' },
]

const versionRows = [
  { label: 'Versión actual', value: '2.4.1' },
  { label: 'Última actualización', value: '28 de abril de 2026' },
  { label: 'Estado', value: 'Operativo', isStatus: true },
  { label: 'Entorno', value: 'Producción' },
  { label: 'Base de datos', value: 'Sincronizada' },
  { label: 'Desarrollado por', value: 'Equipo TI Roemmers' },
]

const contactItems = [
  {
    label: 'Teléfono',
    value: '0800-777-7636',
    icon: `<svg viewBox="0 0 24 24" fill="none" stroke="#1a73e8" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" width="16" height="16"><path d="M22 16.92v3a2 2 0 0 1-2.18 2A19.79 19.79 0 0 1 4 4.18 2 2 0 0 1 6.11 2h3a2 2 0 0 1 2 1.72c.127.96.361 1.903.7 2.81a2 2 0 0 1-.45 2.11L10.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45c.907.339 1.85.573 2.81.7A2 2 0 0 1 22 16.92z"/></svg>`,
  },
  {
    label: 'Email',
    value: 'sistemas@roemmers.com.ar',
    icon: `<svg viewBox="0 0 24 24" fill="none" stroke="#1a73e8" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" width="16" height="16"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>`,
  },
  {
    label: 'Horario',
    value: 'Lunes a viernes, 8–18 hs',
    icon: `<svg viewBox="0 0 24 24" fill="none" stroke="#1a73e8" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" width="16" height="16"><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></svg>`,
  },
]
</script>

<style scoped>
.info-card { max-width: 640px; margin: 20px auto; background: #fff; border: 0.5px solid #e0e0e0; border-radius: 12px; overflow: hidden; }
.info-tabs { display: flex; border-bottom: 0.5px solid #e0e0e0; }
.info-tab { padding: 0.75rem 1.25rem; font-size: 13px; cursor: pointer; color: #666; border: none; border-bottom: 2px solid transparent; background: transparent; transition: all 0.15s; }
.info-tab.active { color: #1a73e8; border-bottom-color: #1a73e8; font-weight: 500; }
.info-panel { padding: 1.5rem 1.75rem; }
.info-logo-row { display: flex; align-items: center; gap: 12px; margin-bottom: 1rem; }
.info-logo-circle { width: 44px; height: 44px; border-radius: 50%; background: #1a73e8; display: flex; align-items: center; justify-content: center; font-size: 11px; color: #fff; }
.info-app-name { font-size: 16px; font-weight: 500; margin: 0; }
.info-app-sub { font-size: 12px; color: #666; margin: 2px 0 0; }
.info-desc { font-size: 13px; color: #555; line-height: 1.6; margin-bottom: 1rem; }
.badge { font-size: 11px; padding: 3px 10px; border-radius: 6px; background: #e8f0fe; color: #1a5bbf; margin-right: 8px; }
.version-table { width: 100%; font-size: 13px; border-collapse: collapse; }
.version-table td { padding: 8px 0; border-bottom: 0.5px solid #e0e0e0; }
.status-dot { display: inline-block; width: 7px; height: 7px; border-radius: 50%; background: #34a853; margin-right: 6px; }
.contact-row { display: flex; align-items: center; gap: 12px; padding: 0.7rem 0; border-bottom: 0.5px solid #e0e0e0; font-size: 13px; }
.contact-icon-wrap { width: 32px; height: 32px; border-radius: 8px; background: #e8f0fe; display: flex; align-items: center; justify-content: center; color: #1a73e8; }
</style>