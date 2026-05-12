<template>
  <footer class="footer">
    <div class="footer-links">
      <span class="footer-link" @click="abrirContacto">Contacto</span>
      <span class="separator">|</span>
      <span class="footer-link" @click="abrirSoporte">Soporte</span>
      <span class="separator">|</span>
      <span class="footer-link" @click="abrirInformacion">Información</span>
    </div>
  </footer>

  <ContactoModal v-if="mostrarContacto" @cerrar="cerrarTodos" />

  <div
    v-if="mostrarSoporte"
    class="modal-overlay"
    role="dialog"
    aria-modal="true"
    aria-labelledby="footer-soporte-title"
    @click.self="cerrarTodos"
  >
    <div class="modal-card modal-card--scroll">
      <button type="button" class="btn-close" aria-label="Cerrar" @click="cerrarTodos">✕</button>
      <h2 id="footer-soporte-title" class="modal-sr-only">Soporte</h2>
      <SoporteSection />
    </div>
  </div>

  <div
    v-if="mostrarInformacion"
    class="modal-overlay"
    role="dialog"
    aria-modal="true"
    aria-labelledby="footer-info-title"
    @click.self="cerrarTodos"
  >
    <div class="modal-card modal-card--scroll">
      <button type="button" class="btn-close" aria-label="Cerrar" @click="cerrarTodos">✕</button>
      <h2 id="footer-info-title" class="modal-sr-only">Información</h2>
      <InformacionSection />
    </div>
  </div>
</template>

<script>
import ContactoModal from './ContactoModal.vue'
import SoporteSection from './SoporteSection.vue'
import InformacionSection from './InformacionSection.vue'

export default {
  name: 'FooterComponent',
  components: { ContactoModal, SoporteSection, InformacionSection },
  data() {
    return {
      mostrarContacto: false,
      mostrarSoporte: false,
      mostrarInformacion: false
    }
  },
  methods: {
    cerrarTodos() {
      this.mostrarContacto = false
      this.mostrarSoporte = false
      this.mostrarInformacion = false
    },
    abrirContacto() {
      this.mostrarSoporte = false
      this.mostrarInformacion = false
      this.mostrarContacto = true
    },
    abrirSoporte() {
      this.mostrarContacto = false
      this.mostrarInformacion = false
      this.mostrarSoporte = true
    },
    abrirInformacion() {
      this.mostrarContacto = false
      this.mostrarSoporte = false
      this.mostrarInformacion = true
    }
  }
}
</script>

<style scoped>
.footer {
  width: 100%;
  background-color: #fff;
  padding: 20px 0;
  text-align: center;
  border-top: 1px solid #f0f0f0;
  margin-top: 40px;
}
.footer-links {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 15px;
  color: #777;
}
.footer-link {
  color: #777;
  text-decoration: none;
  font-size: 0.9rem;
  cursor: pointer;
  transition: color 0.2s;
}
.footer-link:hover {
  color: #1a73e8;
  text-decoration: underline;
}
.separator {
  color: #ccc;
}

.modal-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.35);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
  padding: 24px 16px;
  backdrop-filter: blur(2px);
}
.modal-card {
  background: #fff;
  border-radius: 16px;
  max-width: 680px;
  width: 100%;
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.15);
  position: relative;
  animation: fadeInUp 0.2s ease;
}
.modal-card--scroll {
  max-height: min(90vh, 900px);
  overflow-y: auto;
  padding: 44px 24px 28px;
}
.btn-close {
  position: absolute;
  top: 12px;
  right: 12px;
  z-index: 2;
  background: #fff;
  border: none;
  font-size: 1rem;
  color: #aaa;
  cursor: pointer;
  line-height: 1;
  padding: 8px 10px;
  border-radius: 8px;
}
.btn-close:hover {
  color: #555;
  background: #f5f5f5;
}
.modal-sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.modal-card :deep(.soporte-wrap),
.modal-card :deep(.info-card) {
  margin: 0;
  max-width: none;
}
</style>
