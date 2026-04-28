<template>
  <div class="form-card">
    <h1 class="card-title">Armar Nueva Bolsa</h1>
    
    <div class="form-group">
      <label class="form-label">Nombre del paciente</label>
      <input type="text" class="form-control" />
    </div>
    
    <div class="form-group">
      <label class="form-label">DNI / ID</label>
      <input type="text" class="form-control" />
    </div>
    
    <div class="medications-section">
      <button class="btn btn-secondary">
        <span class="plus-icon">+</span> Agregar medicamento
      </button>
      <ul class="medication-list">
        <li>Paracetamol 500mg</li>
        <li>Ibuprofeno 400mg</li>
      </ul>
    </div>
    
    <div class="action-section">
      <button class="btn btn-primary">Confirmar Bolsa</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BolsaForm'
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
.medications-section {
  margin-top: 25px;
}
.plus-icon {
  font-weight: bold;
  font-size: 1.2rem;
  margin-right: 8px;
}
.medication-list {
  list-style: none;
  padding: 0;
  margin-top: 15px;
  color: #555;
  font-size: 1.1rem;
}
.medication-list li::before {
  content: "•";
  color: #555;
  margin-right: 10px;
}
.action-section {
  text-align: center;
  margin-top: 35px;
}
.btn {
  padding: 12px 30px;
  border-radius: 8px;
  font-size: 1.1rem;
  font-weight: 500;
  cursor: pointer;
  border: none;
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
  border: 1px solid #bbdefb;
}
</style>