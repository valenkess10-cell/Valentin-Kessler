<template>
  <div class="modal-overlay" @click.self="$emit('cerrar')">
    <div class="modal-card">
      <button class="btn-close" @click="$emit('cerrar')">✕</button>

      <div class="modal-hero">
        <div class="hero-icon">📋</div>
        <h2>Información del Sistema</h2>
        <p>Armado de Bolsas — Roemmers</p>
      </div>

      <div class="info-body">

        <div class="info-section">
          <h3 class="section-title">Sobre el sistema</h3>
          <p class="section-text">
            El sistema de <strong>Armado de Bolsas</strong> fue desarrollado para optimizar y digitalizar
            el proceso de preparación de medicamentos por paciente dentro de la operación farmacéutica de Roemmers.
            Permite registrar bolsas, asociar medicamentos con cantidades de cajas y llevar un historial centralizado.
          </p>
        </div>

        <div class="info-grid">
          <div class="info-item">
            <span class="info-icon">🏷️</span>
            <div>
              <p class="info-label">Versión</p>
              <p class="info-value">v1.0.0</p>
            </div>
          </div>
          <div class="info-item">
            <span class="info-icon">📅</span>
            <div>
              <p class="info-label">Fecha de lanzamiento</p>
              <p class="info-value">Mayo 2026</p>
            </div>
          </div>
          <div class="info-item">
            <span class="info-icon">👨‍💻</span>
            <div>
              <p class="info-label">Desarrollador</p>
              <p class="info-value">Kessler Valentín</p>
            </div>
          </div>
          <div class="info-item">
            <span class="info-icon">🏢</span>
            <div>
              <p class="info-label">Empresa</p>
              <p class="info-value">Laboratorio Roemmers S.A.I.C.</p>
            </div>
          </div>
          <div class="info-item">
            <span class="info-icon">⚙️</span>
            <div>
              <p class="info-label">Tecnología</p>
              <p class="info-value">Vue 3 + Vite</p>
            </div>
          </div>
          <div class="info-item">
            <span class="info-icon">🔒</span>
            <div>
              <p class="info-label">Entorno</p>
              <p class="info-value">Uso interno — Confidencial</p>
            </div>
          </div>
        </div>

        <div class="info-section">
          <h3 class="section-title">¿Cómo usar el sistema?</h3>
          <ol class="steps-list">
            <li>Ingresá el <strong>nombre del paciente</strong> y su <strong>DNI</strong> en el formulario principal.</li>
            <li>Agregá los <strong>medicamentos</strong> necesarios indicando la cantidad de cajas (máx. 10 por ítem).</li>
            <li>Presioná <strong>Confirmar Bolsa</strong> para registrarla en el sistema.</li>
            <li>Consultá todas las bolsas creadas desde la sección <strong>Bolsas</strong> en el menú superior.</li>
          </ol>
        </div>

        <div class="disclaimer">
          © 2025 Laboratorio Roemmers S.A.I.C. — Todos los derechos reservados.
        </div>

      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'InformacionModal',
  emits: ['cerrar']
}
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,0.4);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
  backdrop-filter: blur(2px);
}
.modal-card {
  background: #fff;
  border-radius: 16px;
  max-width: 620px;
  width: 92%;
  max-height: 88vh;
  overflow-y: auto;
  box-shadow: 0 20px 50px rgba(0,0,0,0.15);
  position: relative;
  animation: fadeIn 0.2s ease;
}
@keyframes fadeIn {
  from { opacity: 0; transform: translateY(-10px); }
  to   { opacity: 1; transform: translateY(0); }
}
.btn-close {
  position: absolute;
  top: 14px;
  right: 18px;
  background: rgba(255,255,255,0.25);
  border: none;
  font-size: 1rem;
  color: #fff;
  cursor: pointer;
  border-radius: 50%;
  width: 28px;
  height: 28px;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 10;
}
.btn-close:hover { background: rgba(255,255,255,0.4); }

.modal-hero {
  background: linear-gradient(135deg, #2e7d32, #1b5e20);
  color: #fff;
  padding: 28px 30px 22px;
  text-align: center;
}
.hero-icon {
  font-size: 2.2rem;
  margin-bottom: 8px;
}
.modal-hero h2 {
  margin: 0 0 6px;
  font-size: 1.5rem;
  font-weight: 700;
}
.modal-hero p {
  margin: 0;
  font-size: 0.92rem;
  opacity: 0.85;
}

.info-body {
  padding: 24px 28px 28px;
  display: flex;
  flex-direction: column;
  gap: 22px;
}


.section-title {
  font-size: 1rem;
  font-weight: 700;
  color: #2c3e50;
  margin: 0 0 10px;
  padding-bottom: 6px;
  border-bottom: 2px solid #e8f5e9;
}
.section-text {
  font-size: 0.92rem;
  color: #555;
  line-height: 1.6;
  margin: 0;
}

.info-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 10px;
}
.info-item {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 12px 14px;
  background: #f8faf8;
  border: 1px solid #e8f5e9;
  border-radius: 10px;
}
.info-icon { font-size: 1.2rem; flex-shrink: 0; }
.info-label {
  margin: 0 0 2px;
  font-size: 0.72rem;
  color: #999;
  text-transform: uppercase;
  letter-spacing: 0.4px;
}
.info-value {
  margin: 0;
  font-size: 0.92rem;
  font-weight: 600;
  color: #333;
}

.steps-list {
  padding-left: 18px;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 8px;
}
.steps-list li {
  font-size: 0.92rem;
  color: #555;
  line-height: 1.5;
}

.disclaimer {
  text-align: center;
  font-size: 0.78rem;
  color: #bbb;
  padding-top: 10px;
  border-top: 1px solid #f0f0f0;
}
</style>
