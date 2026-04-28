<template>
  <div id="app">
    <HeadeComponent />
    <main class="content-wrapper">
      <SystemBanner />
      <BolsaForm />
      <BolsasLista />
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
  }
}
</script>

<style>
/* Estilos globales para toda la aplicación */
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  padding: 0;
  background-color: #f0f4f8; /* El color de fondo azul suave */
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.content-wrapper {
  padding: 20px;
}
</style>