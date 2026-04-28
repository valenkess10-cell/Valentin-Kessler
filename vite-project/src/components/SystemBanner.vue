<template>
  <div class="system-banner">
    <p>Sistema para <strong>armado</strong> y control de bolsas</p>
  </div>
</template>

<script>
export default {
  name: 'SystemBanner'
}
</script>

<style scoped>
.system-banner {
  background-color: #e3f2fd; /* Color celeste del diseño */
  margin: 20px auto;
  padding: 15px;
  border-radius: 8px;
  text-align: center;
  color: #455a64;
  font-size: 1.1rem;
  max-width: 800px;
}

.system-banner strong {
  font-weight: bold;
}
</style>