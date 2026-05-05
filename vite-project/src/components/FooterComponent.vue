<template>
  <footer class="footer">
    <div class="footer-links">
      <span class="footer-link" @click="mostrarContacto = true">Contacto</span>
      <span class="separator">|</span>
      <a href="#" class="footer-link">Soporte</a>
      <span class="separator">|</span>
      <a href="#" class="footer-link">Información</a>
    </div>
  </footer>

  <ContactoModal v-if="mostrarContacto" @cerrar="mostrarContacto = false" />
</template>

<script>
import ContactoModal from './ContactoModal.vue'

export default {
  name: 'FooterComponent',
  components: { ContactoModal },
  data() {
    return {
      mostrarContacto: false
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
</style>
