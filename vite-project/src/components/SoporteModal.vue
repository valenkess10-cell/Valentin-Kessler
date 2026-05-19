<template>
  <div class="modal-overlay" @click.self="$emit('cerrar')">
    <div class="modal-card">
      <button class="btn-close" @click="$emit('cerrar')">✕</button>

      <div class="modal-hero">
        <h2>Centro de soporte</h2>
        <p>¿Necesitás ayuda? Elegí una opción o envianos tu consulta.</p>
      </div>

      <div class="opciones-grid">
        <div class="opcion-card">
          <div class="opcion-icon">💬</div>
          <div>
            <p class="opcion-titulo">Chat en vivo</p>
            <p class="opcion-sub">Respuesta inmediata</p>
          </div>
        </div>
        <a href="tel:3804936965" class="opcion-card">
          <div class="opcion-icon">📞</div>
          <div>
            <p class="opcion-titulo">Llamar al soporte</p>
            <p class="opcion-sub">3804936965</p>
          </div>
        </a>
        <a href="mailto:valenkess10@gmail.com" class="opcion-card">
          <div class="opcion-icon">✉️</div>
          <div>
            <p class="opcion-titulo">Enviar por email</p>
            <p class="opcion-sub">valenkess10@gmail.com</p>
          </div>
        </a>
        <div class="opcion-card">
          <div class="opcion-icon">❓</div>
          <div>
            <p class="opcion-titulo">Preguntas frecuentes</p>
            <p class="opcion-sub">Base de conocimiento</p>
          </div>
        </div>
      </div>

      <div class="consulta-section">
        <label class="consulta-label">O describí tu problema y te respondemos a la brevedad</label>
        <textarea
          class="consulta-textarea"
          v-model="consulta"
          placeholder="Ej: No puedo confirmar la bolsa del paciente..."
          rows="4"
        ></textarea>
        <div class="consulta-footer">
          <span class="enviado-msg" v-if="enviado">✅ Consulta enviada. Te responderemos pronto.</span>
          <button class="btn btn-primary" @click="enviarConsulta">Enviar consulta</button>
        </div>
      </div>

    </div>
  </div>
</template>

<script>
export default {
  name: 'SoporteModal',
  emits: ['cerrar'],
  data() {
    return {
      consulta: '',
      enviado: false
    }
  },
  methods: {
    enviarConsulta() {
      if (!this.consulta.trim()) return
      this.enviado = true
      this.consulta = ''
      setTimeout(() => { this.enviado = false }, 4000)
    }
  }
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
  max-width: 600px;
  width: 92%;
  box-shadow: 0 20px 50px rgba(0,0,0,0.15);
  position: relative;
  overflow: hidden;
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
  background: linear-gradient(135deg, #1a73e8, #0d47a1);
  color: #fff;
  padding: 28px 30px 24px;
}
.modal-hero h2 {
  margin: 0 0 6px 0;
  font-size: 1.5rem;
  font-weight: 700;
}
.modal-hero p {
  margin: 0;
  font-size: 0.95rem;
  opacity: 0.88;
}

.opciones-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 12px;
  padding: 24px 28px 10px;
}
.opcion-card {
  display: flex;
  align-items: center;
  gap: 14px;
  padding: 14px 16px;
  border: 1.5px solid #e8eef8;
  border-radius: 10px;
  cursor: pointer;
  text-decoration: none;
  transition: border-color 0.2s, box-shadow 0.2s;
  background: #fff;
}
.opcion-card:hover {
  border-color: #1a73e8;
  box-shadow: 0 2px 8px rgba(26,115,232,0.1);
}
.opcion-icon {
  font-size: 1.4rem;
  flex-shrink: 0;
}
.opcion-titulo {
  margin: 0;
  font-size: 0.95rem;
  font-weight: 600;
  color: #2c3e50;
}
.opcion-sub {
  margin: 2px 0 0;
  font-size: 0.8rem;
  color: #888;
}

.consulta-section {
  padding: 16px 28px 28px;
}
.consulta-label {
  display: block;
  font-size: 0.9rem;
  color: #555;
  margin-bottom: 10px;
}
.consulta-textarea {
  width: 100%;
  padding: 12px 14px;
  border: 1.5px solid #ddd;
  border-radius: 8px;
  font-size: 0.95rem;
  resize: vertical;
  font-family: inherit;
  box-sizing: border-box;
  transition: border-color 0.2s;
}
.consulta-textarea:focus {
  outline: none;
  border-color: #1a73e8;
  box-shadow: 0 0 0 3px rgba(26,115,232,0.1);
}
.consulta-footer {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  gap: 16px;
  margin-top: 12px;
}
.enviado-msg {
  font-size: 0.88rem;
  color: #2e7d32;
}
.btn {
  padding: 11px 26px;
  border-radius: 8px;
  font-size: 0.95rem;
  font-weight: 500;
  cursor: pointer;
  border: none;
  transition: opacity 0.2s;
}
.btn:hover { opacity: 0.88; }
.btn-primary {
  background-color: #1a73e8;
  color: #fff;
}
</style>
