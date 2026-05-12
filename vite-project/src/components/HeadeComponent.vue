<template>
  <nav class="navbar">
    <div class="logo-section">
      <img src="/logo-roemmers.png" alt="Roemmers" class="logo-img" />
      <div class="brand-text">
        <span class="main-title">Armado de Bolsas</span>
        <span class="sub-title">ROEMMERS</span>
      </div>
    </div>
    <ul class="nav-menu">
      <li
        class="nav-link"
        :class="{ active: vistaActiva === 'inicio' }"
        @click="$emit('cambiar-vista', 'inicio')"
      >Inicio</li>
      <li
        class="nav-link"
        :class="{ active: vistaActiva === 'bolsas' }"
        @click="$emit('cambiar-vista', 'bolsas')"
      >Bolsas</li>
      <li class="nav-link dropdown">
        Ayuda <span class="arrow">▾</span>
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  name: 'HeadeComponent',
  props: {
    vistaActiva: {
      type: String,
      default: 'inicio'
    }
  },
  emits: ['cambiar-vista']
}
</script>

<style scoped>
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 15px 50px;
  background-color: #fff;
  border-bottom: 1px solid #f0f0f0;
  font-family: 'Segoe UI', Roboto, sans-serif;
}
.logo-section {
  display: flex;
  align-items: center;
}
.logo-img {
  height: 45px;
  margin-right: 12px;
}
.brand-text {
  display: flex;
  flex-direction: column;
}
.main-title {
  font-size: 1.4rem;
  font-weight: 500;
  color: #333;
}
.sub-title {
  font-size: 0.7rem;
  font-weight: 900;
  color: #333;
  margin-top: -4px;
}
.nav-menu {
  list-style: none;
  display: flex;
  gap: 30px;
  margin: 0;
}
.nav-link {
  color: #666;
  font-weight: 500;
  cursor: pointer;
  padding: 5px 0;
  transition: color 0.2s;
}
.nav-link:hover {
  color: #1a73e8;
}
.nav-link.active {
  color: #1a73e8;
  border-bottom: 3px solid #1a73e8;
}
.arrow {
  font-size: 0.8rem;
}
</style>
