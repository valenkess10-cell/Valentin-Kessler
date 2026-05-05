<template>
  <div class="form-card">
    <h1 class="card-title">Armar Nueva Bolsa</h1>

    <div class="form-group">
      <label class="form-label">Nombre del paciente</label>
      <input type="text" class="form-control" v-model="nombre" placeholder="Ej: Juan Pérez" />
    </div>

    <div class="form-group">
      <label class="form-label">DNI / ID</label>
      <input type="text" class="form-control" v-model="dni" placeholder="Ej: 28.341.120" />
    </div>

    <div class="medications-section">
      <div class="add-med-row">
        <input
          type="text"
          class="form-control med-input"
          v-model="nuevoMedicamento"
          placeholder="Ej: Amoxicilina 500mg"
          @keyup.enter="agregarMedicamento"
        />
        <button class="btn btn-secondary" @click="agregarMedicamento">
          <span class="plus-icon">+</span> Agregar
        </button>
      </div>

      <ul class="medication-list" v-if="medicamentos.length > 0">
        <li v-for="(med, index) in medicamentos" :key="index">
          <span>{{ med }}</span>
          <button class="btn-remove" @click="eliminarMedicamento(index)" title="Eliminar">✕</button>
        </li>
      </ul>
      <p class="empty-meds" v-else>Aún no se agregaron medicamentos.</p>
    </div>

    <p class="error-msg" v-if="errorMsg">{{ errorMsg }}</p>

    <div class="action-section">
      <button class="btn btn-primary" @click="confirmarBolsa">Confirmar Bolsa</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BolsaForm',
  emits: ['bolsa-confirmada'],
  data() {
    return {
      nombre: '',
      dni: '',
      nuevoMedicamento: '',
      medicamentos: [],
      errorMsg: ''
    }
  },
  methods: {
    agregarMedicamento() {
      const med = this.nuevoMedicamento.trim()
      if (!med) return
      this.medicamentos.push(med)
      this.nuevoMedicamento = ''
      this.errorMsg = ''
    },
    eliminarMedicamento(index) {
      this.medicamentos.splice(index, 1)
    },
    confirmarBolsa() {
      if (!this.nombre.trim()) {
        this.errorMsg = 'Por favor ingresá el nombre del paciente.'
        return
      }
      if (!this.dni.trim()) {
        this.errorMsg = 'Por favor ingresá el DNI / ID.'
        return
      }
      if (this.medicamentos.length === 0) {
        this.errorMsg = 'Agregá al menos un medicamento.'
        return
      }
      this.$emit('bolsa-confirmada', {
        nombre: this.nombre.trim(),
        dni: this.dni.trim(),
        medicamentos: [...this.medicamentos]
      })
      // Reset form
      this.nombre = ''
      this.dni = ''
      this.medicamentos = []
      this.errorMsg = ''
    }
  }
}
</script>

<style scoped>
.form-card {
  background-color: #fff;
  padding: 30px;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.08);
  max-width: 600px;
  margin: 0 auto;
}
.card-title {
  text-align: center;
  font-size: 2rem;
  font-weight: 500;
  color: #2c3e50;
  margin-bottom: 30px;
}
.form-group {
  margin-bottom: 20px;
}
.form-label {
  display: block;
  font-size: 1.1rem;
  color: #333;
  margin-bottom: 8px;
}
.form-control {
  width: 100%;
  padding: 12px;
  border: 1px solid #ccc;
  border-radius: 6px;
  background-color: #fcfcfc;
  font-size: 1rem;
}
.form-control:focus {
  outline: none;
  border-color: #1a73e8;
  box-shadow: 0 0 0 3px rgba(26,115,232,0.1);
}
.medications-section {
  margin-top: 25px;
}
.add-med-row {
  display: flex;
  gap: 10px;
  align-items: center;
}
.med-input {
  flex: 1;
}
.medication-list {
  list-style: none;
  padding: 0;
  margin-top: 15px;
  color: #555;
  font-size: 1rem;
}
.medication-list li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 8px 12px;
  background-color: #f5f5f5;
  border-radius: 6px;
  margin-bottom: 6px;
}
.btn-remove {
  background: none;
  border: none;
  color: #e53935;
  cursor: pointer;
  font-size: 0.85rem;
  padding: 2px 6px;
  border-radius: 4px;
  transition: background 0.2s;
}
.btn-remove:hover {
  background-color: #fdecea;
}
.empty-meds {
  color: #aaa;
  font-size: 0.95rem;
  margin-top: 12px;
  text-align: center;
}
.error-msg {
  color: #e53935;
  font-size: 0.95rem;
  text-align: center;
  margin-top: 15px;
}
.action-section {
  text-align: center;
  margin-top: 30px;
}
.btn {
  padding: 12px 30px;
  border-radius: 8px;
  font-size: 1rem;
  font-weight: 500;
  cursor: pointer;
  border: none;
  transition: opacity 0.2s;
}
.btn:hover {
  opacity: 0.88;
}
.btn-primary {
  background-color: #1a73e8;
  color: #fff;
}
.btn-secondary {
  background-color: #e3f2fd;
  color: #1a73e8;
  display: flex;
  align-items: center;
  gap: 6px;
  border: 1px solid #bbdefb;
  white-space: nowrap;
}
.plus-icon {
  font-weight: bold;
  font-size: 1.1rem;
}
</style>
