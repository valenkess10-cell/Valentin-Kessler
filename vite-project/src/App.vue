<template>
  <div id="app">
    <HeadeComponent :vistaActiva="vistaActual" @cambiar-vista="vistaActual = $event" />
    <main class="content-wrapper">
      <SystemBanner />

      <!-- Vista: Inicio -->
      <template v-if="vistaActual === 'inicio'">
        <BolsaForm @bolsa-confirmada="agregarBolsa" />
      </template>

      <!-- Vista: Bolsas -->
      <template v-else-if="vistaActual === 'bolsas'">
        <BolsasLista :bolsas="bolsas" />
      </template>
    </main>
    <FooterComponent />
  </div>
</template>

<script>
import HeadeComponent from './components/HeadeComponent.vue'
import SystemBanner from './components/SystemBanner.vue'
import BolsaForm from './components/BolsaForm.vue'
import BolsasLista from './components/BolsasLista.vue'
import FooterComponent from './components/FooterComponent.vue'

export default {
  name: 'App',
  components: {
    HeadeComponent,
    SystemBanner,
    BolsaForm,
    BolsasLista,
    FooterComponent
  },
  data() {
    return {
      vistaActual: 'inicio',
      bolsas: []
    }
  },
  methods: {
    agregarBolsa(bolsa) {
      this.bolsas.push(bolsa)
      this.vistaActual = 'bolsas' // Redirige a la lista luego de confirmar
    }
  }
}
</script>

<style>
* {
  box-sizing: border-box;
}
body {
  margin: 0;
  padding: 0;
  background-color: #f0f4f8;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}
.content-wrapper {
  padding: 20px;
}
</style>
