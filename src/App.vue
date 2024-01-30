<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <div id="app">
    <form @submit.prevent="enviarFormulario" ref="miFormulario" class="contenedor-formulario">
      <div class="grupo-formulario">
        <h2>FORMULARIO DE USUARIO</h2>
        <label for="nombre">NOMBRE</label>
        <input type="text" id="nombre" v-model="nombre" maxlength="18" placeholder="Juan" required>
      </div>

      <div class="grupo-formulario">
        <label for="apellido">APELLIDO</label>
        <input type="text" id="apellido" v-model="apellido" maxlength="18" placeholder="Pérez" required>
      </div>

      <div class="grupo-formulario">
        <label for="edad">EDAD</label>
        <input type="number" id="edad" v-model="edad" min="0" max="60" pattern="\d*" title="Solo se permiten números" placeholder="22" required>
      </div>

      <div class="grupo-formulario">
        <label for="genero">GÉNERO</label>
        <select id="genero" v-model="genero" placeholder="Masculino" required>
          <option value="Masculino">Masculino</option>
          <option value="Femenino">Femenino</option>
          <option value="Otro">Prefiero no especificar</option>
        </select>
      </div>
      
      <div class="grupo-formulario">
        <label for="telefono">TELÉFONO</label>
        <input type="tel" id="telefono" v-model="telefono" maxlength="10" placeholder="1212121212" required>
      </div>

      <button type="submit" class="enviar">Enviar</button>
    </form>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  data() {
    return {
      nombre: '',
      apellido: '',
      edad: '',
      genero: '',
      telefono: '',
    };
  },
  methods: {
    enviarFormulario() {
      // Validar que la edad tenga dos dígitos
      if (!/^\d{2}$/.test(this.edad)) {
        alert('La edad debe tener exactamente dos dígitos.');
        return;
      }

      // Validar nombre y apellido
      if (this.nombre.trim().toLowerCase() === this.apellido.trim().toLowerCase()) {
        alert('El nombre y el apellido deben ser diferentes.');
        return;
      }

      // Restablecer formulario
      (this.$refs.miFormulario as HTMLFormElement).reset();

      // Limpiar formulario
      this.nombre = '';
      this.apellido = '';
      this.edad = '';
      this.genero = '';
      this.telefono = '';

      alert('Formulario enviado :D');
    },
  },
});
</script>

<style scoped>
#app {
  margin-left: 350px;
  align-items: center;
  height: 80vh; 
  margin-top: 0%;
}

h2 {
  margin-bottom: 20px;
  text-align: center;
  letter-spacing: 4px;
}

.contenedor-formulario {
  text-align: left;
  border: 0.5px solid #ff00cc;
  padding: 20px;
  border-radius: 10px;
  width: 500px;
  max-width: 100%;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  letter-spacing: 4px;
  margin-top: 0%;
}

.grupo-formulario {
  margin-bottom: 10px;
}

label {
  display: block;
  margin-bottom: 8px;
}

input, select {
  width: calc(100% - 16px);
  padding: 8px;
  box-sizing: border-box;
  border: 1px solid #ff00cc;
  border-radius: 4px;
  font-size: 16px;
  margin-top: 4px;
  letter-spacing: 4px;
}

.enviar {
  background-color: #cb78d9;
  color: white;
  padding: 10px 20px;
  font-size: 16px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  margin-left: 330px;
  margin-right: 20px; 
  letter-spacing: 4px;
}

.enviar:hover {
  background-color: #ec1aa6;
}
</style>
