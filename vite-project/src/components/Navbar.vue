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
        <li class="nav-item active">Inicio</li>
        <li class="nav-item">Bolsas</li>
        <li class="nav-item dropdown">
          Ayuda 
          <span class="arrow-down"></span>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'Navbar'
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
  color: #333;
  margin-top: -5px;
}

.nav-links {
  list-style: none;
  display: flex;
  gap: 2rem;
  margin: 0;
  padding: 0;
}

.nav-item {
  color: #555;
  cursor: pointer;
  font-weight: 500;
  padding-bottom: 5px;
  transition: color 0.3s;
}

.nav-item:hover {
  color: #0056b3;
}

.active {
  color: #0056b3;
  border-bottom: 3px solid #0056b3;
}

.dropdown {
  display: flex;
  align-items: center;
}

.arrow-down {
  width: 0; 
  height: 0; 
  border-left: 5px solid transparent;
  border-right: 5px solid transparent;
  border-top: 5px solid #555;
  margin-left: 8px;
}
</style>