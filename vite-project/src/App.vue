<template>
  <div id="app">
    <transition name="fade">
      <Login v-if="!logeado" @login-success="logeado = true" />
    </transition>

    <div v-if="logeado" class="main-layout">
      <HeadeComponent :vistaActiva="vistaActual" @cambiar-vista="actualizarVista" />

      <div class="container">
        <transition name="fade-slide" mode="out-in">
          
          <BolsaForm 
            v-if="vistaActual === 'inicio'" 
            key="inicio"
            @bolsa-confirmada="agregarBolsa" 
          />

          <BolsasLista 
            v-else-if="vistaActual === 'bolsas'" 
            key="bolsas"
            :bolsas="bolsas" 
          />

          <Ayuda 
            v-else-if="vistaActual === 'ayuda'" 
            key="ayuda"
          />

        </transition>
      </div>

      <FooterComponent />
    </div>
  </div>
</template>

<script>
import Login from './components/Login.vue'
import HeadeComponent from './components/HeadeComponent.vue'
import BolsaForm from './components/BolsaForm.vue'
import BolsasLista from './components/BolsasLista.vue'
import Ayuda from './components/Ayuda.vue'
import FooterComponent from './components/FooterComponent.vue'

export default {
  name: 'App',
  components: {
    Login,
    HeadeComponent,
    BolsaForm,
    BolsasLista,
    Ayuda,
    FooterComponent
  },
  data() {
    return {
      logeado: false,     // Controla el acceso previo al sistema
      vistaActual: 'inicio', // Controla la pestaña activa ('inicio', 'bolsas', 'ayuda')
      bolsas: []            // Array global donde se acumulan tus bolsas dinámicas
    }
  },
  methods: {
    actualizarVista(nuevaVista) {
      this.vistaActual = nuevaVista;
    },
    agregarBolsa(nuevaBolsa) {
      this.bolsas.push(nuevaBolsa);
      this.vistaActual = 'bolsas'; // Te redirecciona al listado oficial al guardar
    }
  }
}
</script>

<style>
/* --- ESTILOS BASE Y ESTRUCTURA GENERAL --- */
body {
  margin: 0;
  padding: 0;
  background-color: #f8fafc;
}

#app {
  min-height: 100vh;
}

.main-layout {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 30px 20px;
  width: 100%;
  box-sizing: border-box;
  overflow: hidden; /* Evita scrolls molestos durante las transiciones de componentes */
}

/* --- ANIMACIÓN 1: SALIDA DEL LOGIN (Fade) --- */
.fade-leave-active {
  transition: opacity 0.5s ease;
}
.fade-leave-to {
  opacity: 0;
}

/* --- ANIMACIÓN 2: CAMBIO DE SECCIÓN (Fade & Slide) --- */
.fade-slide-enter-active,
.fade-slide-leave-active {
  transition: all 0.4s ease;
}

/* Estado inicial cuando entra una pestaña (aparece desde abajo y transparente) */
.fade-slide-enter-from {
  opacity: 0;
  transform: translateY(20px);
}

/* Estado final cuando sale una pestaña (se va hacia arriba y se desvanece) */
.fade-slide-leave-to {
  opacity: 0;
  transform: translateY(-20px);
}
</style>