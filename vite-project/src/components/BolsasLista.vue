<template>
  <div class="list-card">
    <h2 class="card-subtitle">Bolsas ya Creadas</h2>
    <div class="list-group">
      <div class="list-item">
        <span class="item-icon">-</span> Juan Pérez <span class="arrow-right">→</span> 3 medicamentos
      </div>
      <div class="list-item">
        <span class="item-icon">-</span> Máia López <span class="arrow-right">→</span> 5 medicamentos
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BolsasLista'
}
</script>

<style scoped>
.list-card {
  background-color: #fff;
  padding: 20px 30px;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.08);
  max-width: 800px;
  margin: 30px auto;
}
.card-subtitle {
  font-size: 1.3rem;
  font-weight: 500;
  color: #333;
  margin-bottom: 15px;
  border-bottom: 1px solid #f0f0f0;
  padding-bottom: 10px;
}
.list-group {
  color: #555;
  font-size: 1.1rem;
}
.list-item {
  padding: 10px 0;
  display: flex;
  align-items: center;
}
.item-icon {
  margin-right: 10px;
}
.arrow-right {
  margin: 0 10px;
  color: #999;
}
</style>