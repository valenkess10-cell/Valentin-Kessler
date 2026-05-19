<template>
  <div class="ayuda-container">
    <div class="help-card">
      <h1 class="page-title">Centro de Ayuda y Soporte</h1>
      <p class="subtitle">Sistema para armado y control de bolsas (Roemmers)</p>

      <div class="info-section">
        <h2 class="section-title">📋 ¿Cómo armar una nueva bolsa?</h2>
        <ol class="steps-list">
          <li>Ingrese el <strong>Nombre del paciente</strong> completo en el campo de texto.</li>
          <li>Escriba el número de <strong>DNI / ID</strong> para garantizar la trazabilidad.</li>
          <li>Busque el medicamento, elija la cantidad de cajas y presione el botón <strong>+ Agregar</strong>.</li>
          <li>Una vez cargada toda la lista en la parte inferior, haga clic en el botón azul <strong>Confirmar Bolsa</strong>.</li>
        </ol>
      </div>

      <div class="info-section">
        <h2 class="section-title">❓ Preguntas Frecuentes</h2>
        <div class="faqs-list">
          <div v-for="(faq, index) in faqs" :key="index" class="faq-item">
            <button class="faq-toggle" @click="toggleFaq(index)">
              <span class="faq-question">{{ faq.pregunta }}</span>
              <span class="faq-arrow">{{ faq.abierto ? '▲' : '▼' }}</span>
            </button>
            <div v-if="faq.abierto" class="faq-answer">
              <p>{{ faq.respuesta }}</p>
            </div>
          </div>
        </div>
      </div>

      <div class="soporte-box">
        <h3>¿Necesitás asistencia técnica inmediata?</h3>
        <p>Comunicate con el área de soporte informático de Laboratorios Roemmers.</p>
        <div class="soporte-actions">
          <span class="soporte-telefono">📞 3804936965 (Soporte)</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Ayuda',
  data() {
    return {
      faqs: [
        {
          pregunta: '¿Qué hago si un medicamento no aparece en el buscador?',
          respuesta: 'Verifique que el nombre comercial o genérico esté bien escrito. Si el fármaco es de reciente incorporación, comuníquese con Farmacia para darlo de alta en el sistema.',
          abierto: false
        },
        {
          pregunta: '¿Puedo modificar una bolsa después de hacer clic en Confirmar?',
          respuesta: 'Una vez confirmada, la bolsa se envía al listado oficial. Para modificaciones críticas de seguridad o cancelaciones por error, avise de inmediato al supervisor de turno.',
          abierto: false
        },
        {
          pregunta: '¿El campo DNI / ID es obligatorio?',
          respuesta: 'Sí, es un requisito mandatorio indispensable para asegurar la trazabilidad del medicamento y evitar errores en la entrega final al paciente.',
          abierto: false
        }
      ]
    }
  },
  methods: {
    toggleFaq(index) {
      this.faqs[index].abierto = !this.faqs[index].abierto;
    }
  }
}
</script>

<style scoped>
.ayuda-container {
  display: flex;
  justify-content: center;
  padding: 10px 0;
  font-family: 'Segoe UI', Roboto, sans-serif;
}

.help-card {
  background: #ffffff;
  border-radius: 12px;
  box-shadow: 0 4px 14px rgba(0, 0, 0, 0.06);
  padding: 30px;
  width: 100%;
  max-width: 750px;
}

.page-title {
  font-size: 1.6rem;
  color: #2c3e50;
  margin: 0 0 6px 0;
  text-align: center;
}

.subtitle {
  font-size: 0.9rem;
  color: #666;
  text-align: center;
  margin: 0 0 30px 0;
}

.info-section {
  margin-bottom: 25px;
}

.section-title {
  font-size: 1.1rem;
  font-weight: 600;
  color: #1a73e8;
  border-bottom: 1px solid #edf2f7;
  padding-bottom: 8px;
  margin-bottom: 12px;
}

.steps-list {
  padding-left: 20px;
  color: #4a5568;
  font-size: 0.92rem;
  line-height: 1.6;
}

.steps-list li {
  margin-bottom: 8px;
}

.faqs-list {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.faq-item {
  border: 1px solid #e2e8f0;
  border-radius: 8px;
  overflow: hidden;
}

.faq-toggle {
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #f8fafc;
  border: none;
  padding: 12px 16px;
  text-align: left;
  cursor: pointer;
}

.faq-toggle:hover {
  background: #edf2f7;
}

.faq-question {
  font-size: 0.92rem;
  font-weight: 600;
  color: #2d3748;
}

.faq-arrow {
  font-size: 0.75rem;
  color: #718096;
}

.faq-answer {
  padding: 12px 16px;
  background: #ffffff;
  border-top: 1px solid #e2e8f0;
  font-size: 0.88rem;
  color: #4a5568;
  line-height: 1.5;
}

.soporte-box {
  background: #f0f7ff;
  border: 1px solid #e1effe;
  border-radius: 8px;
  padding: 20px;
  text-align: center;
  margin-top: 30px;
}

.soporte-box h3 {
  margin: 0 0 6px 0;
  font-size: 1rem;
  color: #1e3a8a;
}

.soporte-box p {
  margin: 0 0 16px 0;
  font-size: 0.85rem;
  color: #1e40af;
}

.soporte-actions {
  display: flex;
  justify-content: center;
  align-items: center;
}

.soporte-telefono {
  font-size: 1rem;
  color: #1e3a8a;
  font-weight: 600;
  background-color: #fff;
  padding: 8px 16px;
  border: 1px solid #b9ddff;
  border-radius: 6px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.02);
}
</style>