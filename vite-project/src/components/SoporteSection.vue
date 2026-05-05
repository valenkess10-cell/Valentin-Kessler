<template>
  <div class="soporte-wrap">
    <div class="soporte-header">
      <h2>Centro de soporte</h2>
      <p>¿Necesitás ayuda? Elegí una opción o envianos tu consulta[cite: 7].</p>
    </div>

    <div class="soporte-body">
      <!-- Tarjetas de acceso rápido -->
      <div v-for="card in cards" :key="card.title" class="soporte-card">
        <div class="soporte-icon">
          <component :is="card.icon" />
        </div>
        <div>
          <p class="soporte-card-title">{{ card.title }}</p>
          <p class="soporte-card-sub">{{ card.sub }}</p>
        </div>
      </div>

      <div class="soporte-divider" />

      <!-- Formulario de consulta -->
      <div class="soporte-form-row">
        <label>O describí tu problema y te respondemos a la brevedad</label>
        <textarea
          v-model="mensaje"
          placeholder="Ej: No puedo confirmar la bolsa del paciente..."
        />
        <button class="btn-primary" :class="{ sent: enviado }" @click="enviar">
          {{ enviado ? 'Enviado ✓' : 'Enviar consulta' }}
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, defineComponent, h } from 'vue'

const mensaje = ref('')
const enviado = ref(false)

function enviar() {
  if (!mensaje.value.trim()) return
  enviado.value = true
  setTimeout(() => { enviado.value = false; mensaje.value = ''; }, 3000)
}

// Iconos SVG definidos como componentes
const IconChat = defineComponent({ render: () => h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '2' }, [h('path', { d: 'M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z' })]) })
const IconPhone = defineComponent({ render: () => h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '2' }, [h('path', { d: 'M22 16.92v3a2 2 0 0 1-2.18 2A19.79 19.79 0 0 1 4 4.18 2 2 0 0 1 6.11 2h3a2 2 0 0 1 2 1.72c.127.96.361 1.903.7 2.81a2 2 0 0 1-.45 2.11L10.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45c.907.339 1.85.573 2.81.7A2 2 0 0 1 22 16.92z' })]) })
const IconMail = defineComponent({ render: () => h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '2' }, [h('path', { d: 'M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z' }), h('polyline', { points: '22,6 12,13 2,6' })]) })
const IconHelp = defineComponent({ render: () => h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '2' }, [h('circle', { cx: '12', cy: '12', r: '10' }), h('path', { d: 'M9.09 9a3 3 0 0 1 5.83 1c0 2-3 3-3 3' }), h('line', { x1: '12', y1: '17', x2: '12.01', y2: '17' })]) })

const cards = [
  { title: 'Chat en vivo', sub: 'Respuesta inmediata', icon: IconChat },
  { title: 'Llamar al soporte', sub: '0800-777-ROEM', icon: IconPhone },
  { title: 'Enviar por email', sub: 'soporte@roemmers.com', icon: IconMail },
  { title: 'Preguntas frecuentes', sub: 'Base de conocimiento', icon: IconHelp },
]
</script>

<style scoped>
.soporte-wrap { max-width: 640px; margin: 20px auto; }
.soporte-header { background: #1a73e8; border-radius: 12px 12px 0 0; padding: 1.5rem; color: #fff; }
.soporte-header h2 { font-size: 18px; font-weight: 500; margin: 0; }
.soporte-header p { font-size: 13px; opacity: 0.9; margin: 4px 0 0; }
.soporte-body { background: #fff; border: 0.5px solid #e0e0e0; border-top: none; border-radius: 0 0 12px 12px; padding: 1.5rem; display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }
.soporte-card { border: 0.5px solid #e0e0e0; border-radius: 8px; padding: 1rem; display: flex; gap: 12px; cursor: pointer; transition: background 0.15s; }
.soporte-card:hover { background: #f9f9f9; }
.soporte-icon { width: 36px; height: 36px; border-radius: 8px; background: #e8f0fe; display: flex; align-items: center; justify-content: center; color: #1a73e8; flex-shrink: 0; }
.soporte-icon svg { width: 18px; height: 18px; }
.soporte-card-title { font-size: 14px; font-weight: 500; margin: 0; }
.soporte-card-sub { font-size: 12px; color: #666; margin: 2px 0 0; }
.soporte-divider { grid-column: 1 / -1; height: 1px; background: #eee; margin: 10px 0; }
.soporte-form-row { grid-column: 1 / -1; display: flex; flex-direction: column; gap: 10px; }
.soporte-form-row label { font-size: 13px; color: #666; }
.soporte-form-row textarea { height: 80px; border: 1px solid #ddd; border-radius: 8px; padding: 10px; font-size: 13px; resize: none; outline: none; }
.soporte-form-row textarea:focus { border-color: #1a73e8; }
.btn-primary { background: #1a73e8; color: #fff; border: none; border-radius: 8px; padding: 10px 20px; cursor: pointer; align-self: flex-end; font-weight: 500; transition: background 0.3s; }
.btn-primary.sent { background: #34a853; }
</style>