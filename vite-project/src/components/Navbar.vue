<template>
  <nav class="navbar">
    <div class="navbar-container">
      <div class="logo-section">
        <img src="@/assets/logo.png" alt="Logo" class="logo-img" />
        <div class="brand-info">
          <span class="brand-name">Armado de Bolsas</span>
          <span class="brand-sub">ROEMMERS</span>
        </div>
      </div>

      <ul class="nav-links">
        <li 
          class="nav-item" 
          :class="{ active: vistaActual === 'inicio' }"
          @click="$emit('cambiar-vista', 'inicio')"
        >
          Inicio
        </li>
        <li 
          class="nav-item" 
          :class="{ active: vistaActual === 'bolsas' }"
          @click="$emit('cambiar-vista', 'bolsas')"
        >
          Bolsas
        </li>
        <li 
          class="nav-item dropdown"
          :class="{ active: vistaActual === 'ayuda' }"
          @click="$emit('cambiar-vista', 'ayuda')"
        >
          Ayuda 
          <span class="arrow-down"></span>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'Navbar',
  props: {
    vistaActual: {
      type: String,
      default: 'inicio'
    }
  },
  emits: ['cambiar-vista']
}
</script>

<style scoped>
.navbar {
  background-color: #ffffff;
  padding: 1rem 2rem;
  box-shadow: 0 2px 4px rgba(0,0,0,0.05);
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.navbar-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 1200px;
  margin: 0 auto;
}

.logo-section {
  display: flex;
  align-items: center;
}

.logo-img {
  height: 40px;
  margin-right: 10px;
}

.brand-info {
  display: flex;
  flex-direction: column;
}

.brand-name {
  font-size: 1.2rem;
  font-weight: 600;
  color: #333;
}

.brand-sub {
  font-size: 0.6rem;
  font-weight: bold;
  letter-spacing: 1px;
  color: #666;
}

.nav-links {
  display: flex;
  list-style: none;
  gap: 20px;
  margin: 0;
  padding: 0;
}

.nav-item {
  font-size: 0.95rem;
  color: #555;
  cursor: pointer;
  padding: 6px 12px;
  border-radius: 4px;
  transition: all 0.2s;
}

.nav-item:hover {
  color: #1a73e8;
  background-color: #f5f8ff;
}

.nav-item.active {
  color: #1a73e8;
  font-weight: 600;
}

.dropdown {
  display: flex;
  align-items: center;
  gap: 4px;
}

.arrow-down {
  display: inline-block;
  width: 0;
  height: 0;
  border-left: 4px solid transparent;
  border-right: 4px solid transparent;
  border-top: 4px solid #555;
}

.nav-item.active .arrow-down {
  border-top-color: #1a73e8;
}
</style>