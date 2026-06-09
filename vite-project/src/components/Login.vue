<template>
  <div class="login-root-container">
    <div class="login-page">
      <div class="shape"></div>
      <div class="shape"></div>

      <div class="login-card">
        <div class="login-header">
          <div class="user-avatar">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor">
              <path d="M12 12c2.7 0 4.8-2.1 4.8-4.8S14.7 2.4 12 2.4 7.2 4.5 7.2 7.2 9.3 12 12 12zm0 2.4c-3.2 0-9.6 1.6-9.6 4.8v2.4h19.2v-2.4c0-3.2-6.4-4.8-9.6-4.8z"/>
            </svg>
          </div>
          <h2>Sistema de Gestión</h2>
          <p v-if="esLogin">Introduce tus credenciales para ingresar</p>
          <p v-else>Crea una cuenta interna de operador</p>
        </div>

        <div class="auth-tabs">
          <button 
            type="button" 
            :class="{ active: esLogin }" 
            @click="cambiarModo(true)"
          >
            Ingresar
          </button>
          <button 
            type="button" 
            :class="{ active: !esLogin }" 
            @click="cambiarModo(false)"
          >
            Registrarse
          </button>
        </div>

        <form v-if="esLogin" @submit.prevent="handleLogin" class="login-form">
          <div class="input-group">
            <label>Usuario</label>
            <input 
              type="text" 
              v-model="user"  
              required
            />
          </div>

          <div class="input-group">
            <label>Contraseña</label>
            <input 
              type="password" 
              v-model="password" 
              
              required
            />
          </div>

          <div v-if="mensajeError" class="login-error-msg">
            {{ mensajeError }}
          </div>

          <button type="submit" class="btn-login">
            Ingresar al Sistema
          </button>
        </form>

        <form v-else @submit.prevent="handleRegister" class="login-form">
          <div class="input-group">
            <label>Nombre Completo</label>
            <input 
              type="text" 
              v-model="regNombre" 
              placeholder="Ej: Valentín Kessler" 
              required
            />
          </div>

          <div class="input-group">
            <label>Nuevo Usuario</label>
            <input 
              type="text" 
              v-model="regUser" 
              placeholder="Ej: valen_k" 
              required
            />
          </div>

          <div class="input-group">
            <label>Contraseña</label>
            <input 
              type="password" 
              v-model="regPassword" 
              placeholder="Mínimo 4 caracteres" 
              required
            />
          </div>

          <div v-if="mensajeError" class="login-error-msg">
            {{ mensajeError }}
          </div>
          
          <div v-if="mensajeExito" class="login-success-msg">
            {{ mensajeExito }}
          </div>

          <button type="submit" class="btn-login btn-register">
            Crear Cuenta
          </button>
        </form>

        <div class="login-footer">
          <span>Laboratorios Roemmers S.A.I.C. — 2026</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Login',
  data() {
    return {
      esLogin: true,
      user: '',
      password: '',
      regNombre: '',
      regUser: '',
      regPassword: '',
      mensajeError: '',
      mensajeExito: '',
      usuariosRegistrados: [
        { usuario: 'admin', clave: '1234', nombre: 'Administrador' }
      ]
    }
  },
  methods: {
    cambiarModo(modo) {
      this.esLogin = modo;
      this.mensajeError = '';
      this.mensajeExito = '';
    },
    handleLogin() {
      const usuarioEncontrado = this.usuariosRegistrados.find(
        u => u.usuario === this.user.trim().toLowerCase() && u.clave === this.password
      );

      if (usuarioEncontrado) {
        this.$emit('login-success');
      } else {
        this.mensajeError = '⚠️ Usuario o contraseña incorrectos';
        setTimeout(() => this.mensajeError = '', 3000);
      }
    },
    handleRegister() {
      const usuarioLimpio = this.regUser.trim().toLowerCase();

      if (this.regPassword.length < 4) {
        this.mensajeError = '⚠️ La contraseña debe tener al menos 4 caracteres';
        return;
      }

      const existe = this.usuariosRegistrados.some(u => u.usuario === usuarioLimpio);
      if (existe) {
        this.mensajeError = '⚠️ Ese nombre de usuario ya está en uso';
        return;
      }

      this.usuariosRegistrados.push({
        usuario: usuarioLimpio,
        clave: this.regPassword,
        nombre: this.regNombre
      });

      this.mensajeError = '';
      this.mensajeExito = '¡Registro completado con éxito! Redirigiendo...';

      this.regNombre = '';
      this.regUser = '';
      this.regPassword = '';

      setTimeout(() => {
        this.cambiarModo(true);
      }, 1500);
    }
  }
}
</script>

<style scoped>
/* Contenedor raíz único para heredar clases de la animación de Vue sin problemas */
.login-root-container {
  width: 100%;
  height: 100%;
}

.login-page {
  height: 100vh;
  width: 100vw;
  background-color: #eef2f7;
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 9999;
  overflow: hidden;
  font-family: 'Segoe UI', sans-serif;
}

.shape {
  height: 250px;
  width: 250px;
  position: absolute;
  border-radius: 50%;
}
.shape:first-child {
  background: linear-gradient(#1a73e8, #64b5f6);
  left: -80px;
  top: -80px;
}
.shape:last-child {
  background: linear-gradient(to right, #42a5f5, #1565c0);
  right: -80px;
  bottom: -80px;
}

.login-card {
  width: 400px;
  background-color: #ffffff;
  border: 1px solid #e0e7ef;
  border-radius: 16px;
  box-shadow: 0 8px 30px rgba(0,0,0,0.1);
  padding: 35px;
  color: #2c3e50;
  z-index: 10;
}

.login-header {
  text-align: center;
  margin-bottom: 20px;
}

.user-avatar {
  width: 72px;
  height: 72px;
  border-radius: 50%;
  background: #e3f2fd;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto 14px;
  border: 2px solid #bbdefb;
}
.user-avatar svg {
  width: 42px;
  height: 42px;
  color: #1a73e8;
}

.login-header h2 {
  font-size: 1.4rem;
  margin: 0;
}

.login-header p {
  font-size: 0.85rem;
  color: #888;
  margin-top: 5px;
}

.auth-tabs {
  display: flex;
  background: #f0f4f8;
  border-radius: 8px;
  margin-bottom: 25px;
  padding: 4px;
}

.auth-tabs button {
  flex: 1;
  background: transparent;
  border: none;
  color: #888;
  padding: 10px;
  cursor: pointer;
  font-weight: 600;
  font-size: 0.9rem;
  border-radius: 6px;
  transition: all 0.2s;
}

.auth-tabs button.active {
  background: #ffffff;
  color: #1a73e8;
  box-shadow: 0 2px 5px rgba(0,0,0,0.1);
}

.login-form {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.input-group {
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.input-group label {
  font-size: 0.85rem;
  font-weight: 500;
  color: #1a73e8;
}

.input-group input {
  background: #fafafa;
  border: 1.5px solid #ddd;
  border-radius: 8px;
  padding: 11px 14px;
  color: #2c3e50;
  outline: none;
  font-size: 0.95rem;
  transition: all 0.3s;
}

.input-group input:focus {
  border-color: #1a73e8;
  background: #fff;
}

.btn-login {
  background: #1a73e8;
  color: #ffffff;
  padding: 12px;
  border: none;
  border-radius: 8px;
  font-size: 0.95rem;
  font-weight: 700;
  cursor: pointer;
  transition: transform 0.2s, background 0.3s;
  margin-top: 5px;
}

.btn-login:hover {
  background: #1558c0;
  transform: translateY(-2px);
}

.btn-register {
  background: linear-gradient(135deg, #23a2f6, #1845ad);
  color: white;
}

.btn-register:hover {
  background: linear-gradient(135deg, #3bb0ff, #1e54d4);
}

.login-error-msg {
  background: rgba(255, 75, 75, 0.2);
  color: #ff8e8e;
  padding: 10px;
  border-radius: 6px;
  font-size: 0.85rem;
  text-align: center;
  border: 1px solid rgba(255, 75, 75, 0.3);
}

.login-success-msg {
  background: rgba(46, 204, 113, 0.2);
  color: #2ecc71;
  padding: 10px;
  border-radius: 6px;
  font-size: 0.85rem;
  text-align: center;
  border: 1px solid rgba(46, 204, 113, 0.3);
}

.login-footer {
  margin-top: 25px;
  text-align: center;
  font-size: 0.75rem;
  color: #aaa;
}
</style>