<template>
  <div class="lista-page">
    <h1 class="page-title">Bolsas Creadas</h1>

    <div class="list-card" v-for="(bolsa, index) in bolsas" :key="index">
      <div class="bolsa-header">
        <div class="bolsa-info">
          <span class="bolsa-nombre">{{ bolsa.nombre }}</span>
          <span class="bolsa-dni">DNI: {{ bolsa.dni }}</span>
        </div>
        <span class="bolsa-badge">{{ bolsa.medicamentos.length }} medicamento{{ bolsa.medicamentos.length !== 1 ? 's' : '' }}</span>
      </div>
      <ul class="med-list">
        <li v-for="(med, i) in bolsa.medicamentos" :key="i">{{ med }}</li>
      </ul>
    </div>

    <div v-if="bolsas.length === 0" class="empty-state">
      No hay bolsas creadas todavía.
    </div>
  </div>
</template>

<script>
export default {
  name: 'BolsasLista',
  props: {
    bolsas: {
      type: Array,
      default: () => []
    }
  }
}
</script>

<style scoped>
.lista-page {
  max-width: 800px;
  margin: 0 auto;
  padding: 10px 0;
}
.page-title {
  font-size: 1.8rem;
  font-weight: 600;
  color: #2c3e50;
  margin-bottom: 25px;
  text-align: center;
}
.list-card {
  background-color: #fff;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.08);
  padding: 20px 25px;
  margin-bottom: 16px;
  transition: box-shadow 0.2s;
}
.list-card:hover {
  box-shadow: 0 6px 18px rgba(0,0,0,0.12);
}
.bolsa-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 12px;
  border-bottom: 1px solid #f0f0f0;
  padding-bottom: 12px;
}
.bolsa-info {
  display: flex;
  flex-direction: column;
}
.bolsa-nombre {
  font-size: 1.15rem;
  font-weight: 600;
  color: #333;
}
.bolsa-dni {
  font-size: 0.85rem;
  color: #888;
  margin-top: 2px;
}
.bolsa-badge {
  background-color: #e3f2fd;
  color: #1a73e8;
  border-radius: 20px;
  padding: 4px 14px;
  font-size: 0.85rem;
  font-weight: 500;
}
.med-list {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}
.med-list li {
  background-color: #f5f5f5;
  color: #555;
  padding: 4px 12px;
  border-radius: 6px;
  font-size: 0.9rem;
}
.empty-state {
  text-align: center;
  color: #aaa;
  font-size: 1.1rem;
  margin-top: 50px;
}
</style>
