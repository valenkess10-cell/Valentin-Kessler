<template>
  <footer class="footer">
    <div class="footer-links">
      <a href="#" class="footer-link">Contacto</a>
      <span class="separator">|</span>
      <a href="#" class="footer-link">Soporte</a>
      <span class="separator">|</span>
      <a href="#" class="footer-link">Información</a>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'FooterComponent'
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
}

.footer-link:hover {
  text-decoration: underline;
}

.separator {
  color: #ccc;
}
</style>