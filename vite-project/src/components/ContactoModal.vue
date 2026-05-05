<template>
  <div class="modal-overlay" @click.self="$emit('cerrar')">
    <div class="modal-card">
      <button class="btn-close" @click="$emit('cerrar')">✕</button>

      <div class="modal-header">
        <div class="avatar">VK</div>
        <h2 class="modal-title">Contacto</h2>
      </div>

      <div class="contact-info">
        <div class="info-row">
          <span class="info-icon">👤</span>
          <div>
            <p class="info-label">Responsable del sistema</p>
            <p class="info-value">Kessler Valentín</p>
          </div>
        </div>

        <div class="info-row">
          <span class="info-icon">📞</span>
          <div>
            <p class="info-label">Teléfono</p>
            <a class="info-value link" href="tel:3804936965">380 493-6965</a>
          </div>
        </div>

        <div class="info-row">
          <span class="info-icon">✉️</span>
          <div>
            <p class="info-label">Correo electrónico</p>
            <a class="info-value link" href="mailto:valenkess10@gmail.com">valenkess10@gmail.com</a>
          </div>
        </div>

        <div class="info-row">
          <span class="info-icon">🏢</span>
          <div>
            <p class="info-label">Área</p>
            <p class="info-value">Sistemas & Operaciones — Roemmers</p>
          </div>
        </div>

        <div class="info-row">
          <span class="info-icon">🕐</span>
          <div>
            <p class="info-label">Horario de atención</p>
            <p class="info-value">Lunes a viernes, 8:00 – 17:00 hs</p>
          </div>
        </div>
      </div>

      <div class="modal-footer">
        <a href="mailto:valenkess10@gmail.com" class="btn btn-primary">Enviar correo</a>
        <button class="btn btn-outline" @click="$emit('cerrar')">Cerrar</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ContactoModal',
  emits: ['cerrar']
}
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,0.35);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
  backdrop-filter: blur(2px);
}
.modal-card {
  background: #fff;
  border-radius: 16px;
  padding: 35px 40px;
  max-width: 480px;
  width: 90%;
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
  top: 15px;
  right: 18px;
  background: none;
  border: none;
  font-size: 1rem;
  color: #aaa;
  cursor: pointer;
}
.btn-close:hover { color: #555; }

.modal-header {
  display: flex;
  align-items: center;
  gap: 16px;
  margin-bottom: 28px;
  border-bottom: 1px solid #f0f0f0;
  padding-bottom: 20px;
}
.avatar {
  width: 52px;
  height: 52px;
  border-radius: 50%;
  background: linear-gradient(135deg, #1a73e8, #0d47a1);
  color: #fff;
  font-weight: 700;
  font-size: 1.1rem;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}
.modal-title {
  font-size: 1.5rem;
  font-weight: 600;
  color: #2c3e50;
  margin: 0;
}

.contact-info {
  display: flex;
  flex-direction: column;
  gap: 16px;
}
.info-row {
  display: flex;
  align-items: flex-start;
  gap: 14px;
  padding: 10px 14px;
  background: #f8fafc;
  border-radius: 10px;
}
.info-icon {
  font-size: 1.2rem;
  margin-top: 2px;
}
.info-label {
  font-size: 0.75rem;
  color: #999;
  margin: 0 0 2px 0;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}
.info-value {
  font-size: 1rem;
  color: #333;
  font-weight: 500;
  margin: 0;
}
.link {
  color: #1a73e8;
  text-decoration: none;
}
.link:hover { text-decoration: underline; }

.modal-footer {
  display: flex;
  gap: 12px;
  justify-content: flex-end;
  margin-top: 28px;
  border-top: 1px solid #f0f0f0;
  padding-top: 20px;
}
.btn {
  padding: 10px 22px;
  border-radius: 8px;
  font-size: 0.95rem;
  font-weight: 500;
  cursor: pointer;
  border: none;
  text-decoration: none;
  transition: opacity 0.2s;
}
.btn:hover { opacity: 0.85; }
.btn-primary {
  background-color: #1a73e8;
  color: #fff;
}
.btn-outline {
  background: none;
  border: 1px solid #ddd;
  color: #555;
}
</style>
