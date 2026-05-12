<template>
  <div class="form-card">
    <h1 class="card-title">Armar Nueva Bolsa</h1>

    <!-- Nombre del paciente -->
    <div class="form-group">
      <label class="form-label">Nombre del paciente</label>
      <input
        type="text"
        class="form-control"
        :class="{ 'input-error': errores.nombre, 'input-ok': nombre.length >= 3 && !errores.nombre }"
        v-model="nombre"
        placeholder="Ej: Juan Pérez"
        @input="validarNombre"
        maxlength="60"
      />
      <div class="field-footer">
        <span class="error-inline" v-if="errores.nombre">{{ errores.nombre }}</span>
        <span class="char-count" :class="{ 'char-warn': nombre.length > 50 }">
          {{ nombre.length }}/60
        </span>
      </div>
    </div>

    <!-- DNI / ID -->
    <div class="form-group">
      <label class="form-label">DNI / ID</label>
      <input
        type="text"
        class="form-control"
        :class="{ 'input-error': errores.dni, 'input-ok': dniValido && !errores.dni }"
        v-model="dni"
        placeholder="Ej: 28341120"
        @input="validarDni"
        maxlength="10"
      />
      <span class="error-inline" v-if="errores.dni">{{ errores.dni }}</span>
    </div>

    <!-- Medicamentos -->
    <div class="form-group">
      <label class="form-label">Medicamentos</label>
      <div class="add-med-row">
        <input
          type="text"
          class="form-control med-input"
          v-model="nuevoMedicamento"
          placeholder="Ej: Amoxicilina 500mg"
          @keyup.enter="agregarMedicamento"
        />
        <div class="cajas-counter">
          <button class="counter-btn" @click="nuevasCajas > 1 ? nuevasCajas-- : null" :disabled="nuevasCajas <= 1">−</button>
          <span class="counter-value">{{ nuevasCajas }}</span>
          <button class="counter-btn" @click="nuevasCajas < 10 ? nuevasCajas++ : null" :disabled="nuevasCajas >= 10">+</button>
        </div>
        <button class="btn btn-secondary" @click="agregarMedicamento">
          <span class="plus-icon">+</span> Agregar
        </button>
      </div>
      <span class="error-inline" v-if="errores.med">{{ errores.med }}</span>

      <ul class="medication-list" v-if="medicamentos.length > 0">
        <li v-for="(med, index) in medicamentos" :key="index">
          <div class="med-info">
            <span class="med-nombre">{{ med.nombre }}</span>
            <span class="med-cajas">📦 {{ med.cajas }} caja{{ med.cajas !== 1 ? 's' : '' }}</span>
          </div>
          <button class="btn-remove" @click="eliminarMedicamento(index)" title="Eliminar">✕</button>
        </li>
      </ul>
      <p class="empty-meds" v-else>Aún no se agregaron medicamentos.</p>
    </div>

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
      nuevasCajas: 1,
      medicamentos: [],
      errores: {
        nombre: '',
        dni: '',
        med: ''
      }
    }
  },
  computed: {
    dniSoloNumeros() {
      return this.dni.replace(/\./g, '')
    },
    dniValido() {
      return /^\d{7,10}$/.test(this.dniSoloNumeros)
    }
  },
  methods: {
    validarNombre() {
      const n = this.nombre.trim()
      if (!n) {
        this.errores.nombre = 'El nombre es obligatorio.'
      } else if (n.length < 3) {
        this.errores.nombre = 'El nombre debe tener al menos 3 caracteres.'
      } else if (!/^[a-zA-ZÀ-ÿ\s]+$/.test(n)) {
        this.errores.nombre = 'El nombre solo puede contener letras.'
      } else {
        this.errores.nombre = ''
      }
    },
    validarDni() {
      // Solo dígitos, luego formatear con puntos
      const soloNums = this.dni.replace(/\D/g, '').slice(0, 8)
      // Formatear: 1-2 dígitos sin punto, luego grupos de 3 con punto
      if (soloNums.length <= 2) {
        this.dni = soloNums
      } else if (soloNums.length <= 5) {
        this.dni = soloNums.slice(0, soloNums.length - 3) + '.' + soloNums.slice(-3)
      } else {
        const parte3 = soloNums.slice(-3)
        const parte2 = soloNums.slice(-6, -3)
        const parte1 = soloNums.slice(0, soloNums.length - 6)
        this.dni = parte1 + '.' + parte2 + '.' + parte3
      }
      if (!soloNums) {
        this.errores.dni = 'El DNI es obligatorio.'
      } else if (soloNums.length < 7) {
        this.errores.dni = 'El DNI debe tener al menos 7 dígitos.'
      } else {
        this.errores.dni = ''
      }
    },
    agregarMedicamento() {
      const med = this.nuevoMedicamento.trim()
      if (!med) {
        this.errores.med = 'Escribí el nombre del medicamento.'
        return
      }
      const cajas = Math.min(10, Math.max(1, parseInt(this.nuevasCajas) || 1))
      this.medicamentos.push({ nombre: med, cajas })
      this.nuevoMedicamento = ''
      this.nuevasCajas = 10
      this.errores.med = ''
    },
    eliminarMedicamento(index) {
      this.medicamentos.splice(index, 1)
    },
    confirmarBolsa() {
      this.validarNombre()
      this.validarDni()

      if (this.errores.nombre || this.errores.dni) return
      if (this.medicamentos.length === 0) {
        this.errores.med = 'Agregá al menos un medicamento.'
        return
      }

      this.$emit('bolsa-confirmada', {
        nombre: this.nombre.trim(),
        dni: this.dniSoloNumeros,
        medicamentos: [...this.medicamentos]
      })

      this.nombre = ''
      this.dni = ''
      this.medicamentos = []
      this.errores = { nombre: '', dni: '', med: '' }
    }
  }
}
</script>

<style scoped>
.form-card {
  background-color: #fff;
  padding: 35px 40px;
  border-radius: 14px;
  box-shadow: 0 4px 16px rgba(0,0,0,0.08);
  max-width: 620px;
  margin: 0 auto;
}
.card-title {
  text-align: center;
  font-size: 2rem;
  font-weight: 600;
  color: #2c3e50;
  margin-bottom: 30px;
}
.form-group {
  margin-bottom: 22px;
}
.form-label {
  display: block;
  font-size: 1rem;
  font-weight: 500;
  color: #444;
  margin-bottom: 8px;
}
.form-control {
  width: 100%;
  padding: 11px 14px;
  border: 1.5px solid #ddd;
  border-radius: 8px;
  background-color: #fafafa;
  font-size: 1rem;
  transition: border-color 0.2s, box-shadow 0.2s;
  box-sizing: border-box;
}
.form-control:focus {
  outline: none;
  border-color: #1a73e8;
  box-shadow: 0 0 0 3px rgba(26,115,232,0.1);
}
.input-error {
  border-color: #e53935 !important;
  background-color: #fff8f8;
}
.input-ok {
  border-color: #43a047 !important;
}
.field-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 4px;
}
.char-count {
  font-size: 0.78rem;
  color: #aaa;
  margin-left: auto;
}
.char-warn {
  color: #fb8c00;
  font-weight: 600;
}
.error-inline {
  display: block;
  color: #e53935;
  font-size: 0.85rem;
  margin-top: 4px;
}

/* Medicamentos */
.add-med-row {
  display: flex;
  gap: 10px;
  align-items: center;
}
.med-input {
  flex: 1;
}
.cajas-counter {
  display: flex;
  align-items: center;
  gap: 0;
  border: 1.5px solid #ddd;
  border-radius: 8px;
  overflow: hidden;
  flex-shrink: 0;
  background: #fafafa;
}
.counter-btn {
  background: #f0f4ff;
  border: none;
  width: 34px;
  height: 44px;
  font-size: 1.2rem;
  color: #1a73e8;
  cursor: pointer;
  transition: background 0.15s;
  font-weight: 600;
}
.counter-btn:hover:not(:disabled) {
  background: #dbeafe;
}
.counter-btn:disabled {
  color: #ccc;
  cursor: not-allowed;
  background: #f9f9f9;
}
.counter-value {
  width: 36px;
  text-align: center;
  font-size: 1rem;
  font-weight: 600;
  color: #333;
  user-select: none;
}
.medication-list {
  list-style: none;
  padding: 0;
  margin-top: 12px;
}
.medication-list li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 14px;
  background-color: #f5f8ff;
  border: 1px solid #e3eaff;
  border-radius: 8px;
  margin-bottom: 6px;
}
.med-info {
  display: flex;
  flex-direction: column;
  gap: 2px;
}
.med-nombre {
  font-size: 0.97rem;
  font-weight: 500;
  color: #333;
}
.med-cajas {
  font-size: 0.82rem;
  color: #1a73e8;
}
.btn-remove {
  background: none;
  border: none;
  color: #e53935;
  cursor: pointer;
  font-size: 0.85rem;
  padding: 3px 8px;
  border-radius: 4px;
  transition: background 0.2s;
}
.btn-remove:hover {
  background-color: #fdecea;
}
.empty-meds {
  color: #bbb;
  font-size: 0.92rem;
  margin-top: 12px;
  text-align: center;
}
.action-section {
  text-align: center;
  margin-top: 30px;
}
.btn {
  padding: 12px 32px;
  border-radius: 8px;
  font-size: 1rem;
  font-weight: 500;
  cursor: pointer;
  border: none;
  transition: opacity 0.2s;
}
.btn:hover { opacity: 0.88; }
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
  padding: 11px 18px;
}
.plus-icon {
  font-weight: bold;
  font-size: 1.1rem;
}
</style>
