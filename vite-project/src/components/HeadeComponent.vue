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
      >
        Inicio
      </li>
      <li
        class="nav-link"
        :class="{ active: vistaActiva === 'bolsas' }"
        @click="$emit('cambiar-vista', 'bolsas')"
      >
        Bolsas
      </li>
      <li 
        class="nav-link dropdown"
        :class="{ active: vistaActiva === 'ayuda' }"
        @click="$emit('cambiar-vista', 'ayuda')"
      >
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
  }
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
  font-weight: 600;
  color: #2c3e50;
  line-height: 1.2;
}
.sub-title {
  font-size: 0.65rem;
  font-weight: 700;
  color: #7f8c8d;
  letter-spacing: 1.5px;
}
.nav-menu {
  display: flex;
  list-style: none;
  gap: 30px;
  margin: 0;
  padding: 0;
}
.nav-link {
  font-size: 1rem;
  color: #555;
  cursor: pointer;
  padding: 8px 0;
  font-weight: 500;
  transition: color 0.2s, border-color 0.2s;
  border-bottom: 2px solid transparent;
}
.nav-link:hover {
  color: #1a73e8;
}
.nav-link.active {
  color: #1a73e8;
  border-bottom: 2px solid #1a73e8;
  font-weight: 600;
}
.dropdown {
  display: flex;
  align-items: center;
  gap: 4px;
}
.arrow {
  font-size: 0.8rem;
}
</style>