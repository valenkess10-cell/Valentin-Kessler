<template>
  <div class="lista-page">
    <h1 class="page-title">Bolsas Creadas</h1>

    <div class="list-card" v-for="(bolsa, index) in bolsas" :key="index">
      <div class="bolsa-header">
        <div class="bolsa-info">
          <span class="bolsa-nombre">{{ bolsa.nombre }}</span>
          <span class="bolsa-dni">DNI: {{ formatearDni(bolsa.dni) }}</span>
        </div>
        <div class="badges">
          <span class="bolsa-badge blue">{{ bolsa.medicamentos.length }} medicamento{{ bolsa.medicamentos.length !== 1 ? 's' : '' }}</span>
          <span class="bolsa-badge green">📦 {{ totalCajas(bolsa) }} caja{{ totalCajas(bolsa) !== 1 ? 's' : '' }}</span>
        </div>
      </div>
      <ul class="med-list">
        <li v-for="(med, i) in bolsa.medicamentos" :key="i">
          <span class="med-nombre">{{ med.nombre }}</span>
          <span class="med-cajas">{{ med.cajas }} caja{{ med.cajas !== 1 ? 's' : '' }}</span>
        </li>
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
  },
  methods: {
    formatearDni(dni) {
      const n = String(dni).replace(/\./g, '')
      if (n.length <= 2) return n
      if (n.length <= 5) return n.slice(0, n.length - 3) + '.' + n.slice(-3)
      return n.slice(0, n.length - 6) + '.' + n.slice(-6, -3) + '.' + n.slice(-3)
    },
    totalCajas(bolsa) {
      return bolsa.medicamentos.reduce((sum, m) => sum + (m.cajas || 0), 0)
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
  margin-bottom: 14px;
  border-bottom: 1px solid #f0f0f0;
  padding-bottom: 12px;
}
.bolsa-info {
  display: flex;
  flex-direction: column;
  gap: 3px;
}
.bolsa-nombre {
  font-size: 1.15rem;
  font-weight: 600;
  color: #333;
}
.bolsa-dni {
  font-size: 0.85rem;
  color: #888;
}
.badges {
  display: flex;
  gap: 8px;
}
.bolsa-badge {
  border-radius: 20px;
  padding: 4px 14px;
  font-size: 0.82rem;
  font-weight: 500;
}
.blue {
  background-color: #e3f2fd;
  color: #1a73e8;
}
.green {
  background-color: #e8f5e9;
  color: #2e7d32;
}
.med-list {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 6px;
}
.med-list li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #f5f8ff;
  border: 1px solid #e3eaff;
  padding: 7px 14px;
  border-radius: 8px;
}
.med-nombre {
  color: #444;
  font-size: 0.95rem;
  font-weight: 500;
}
.med-cajas {
  font-size: 0.83rem;
  color: #1a73e8;
  font-weight: 500;
}
.empty-state {
  text-align: center;
  color: #aaa;
  font-size: 1.1rem;
  margin-top: 50px;
}
</style>
