<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <h1 class="text-success p-2">Lista de Tareas de {{ usuario }}</h1>
    <div class="container p-4">
      
      <div class="row">
        <div class="col-6 font-weight-bold text-left">Tareas</div>
        <div class="col-2 font-weight-bold">Estado</div>
        <div class="col-2 font-weight-bold">Eliminar</div>
      </div>

      <div class="row" v-for="(t, index) of tareasFiltradas" :key="t.descripcion">
        <div class="col-6 text-left">{{ t.descripcion }}</div>
        <div class="col-2">
          <input type="checkbox" v-model="t.terminada" class="form-checkbox-input">
        </div>
        <div class="col-2">
          <button class="btn btn-danger btn-xs" @click="eliminarTarea(index)">X</button>
        </div>
      </div>

      <div class="row">
        <div class="col-6 font-weight-bold text-left">
          <input type="text" v-model="nuevaTarea" class="form-control">
        </div>
        <div class="col-2">
          <button class="btn btn-success" @click="agregarTarea">Agregar</button>
        </div>
      </div>
      <div class="row bg-dark py-2 mt-2 text-white">
        <div class="col text-center">
          <input type="checkbox" v-model="ocultarTerminadas" class="form-checkbox-input mr-4" id="ocultarTerminadas">
          <label for="ocultarTerminadas" class="form-checkbox-label font-weight-bold">Ocultar Tareas Terminadas</label>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      usuario : 'Fer',
      tareas : [
        { descripcion : 'Comprar leche', terminadas : 0 },
        { descripcion : 'Comprar pan', terminadas : 0 },
        { descripcion : 'Comprar huevos', terminadas : 0 },
        { descripcion : 'Comprar carne', terminadas : 0 },
        { descripcion : 'Comprar agua', terminadas : 0 },
        { descripcion : 'Comprar aceite', terminadas : 0 },
        { descripcion : 'Comprar sal', terminadas : 0 },
        { descripcion : 'Comprar azucar', terminadas : 0 },
      ],
      ocultarTerminadas : false,
      nuevaTarea : ''
    }
  },
  methods: {
    agregarTarea() {
      this.tareas.push({
        descripcion : this.nuevaTarea,
        terminada : 0
      })
      this.nuevaTarea = '',
      localStorage.setItem('tareas', JSON.stringify(this.tareas))
    },
    eliminarTarea(index) {
      this.tareas.splice(index, 1)
      localStorage.setItem('tareas', JSON.stringify(this.tareas))
    },
  },
  computed : {
    tareasFiltradas() {
      if (this.ocultarTerminadas) {
        return this.tareas.filter(t => !t.terminada)
      } else {
        return this.tareas
      }
    },
  },
  created() {
    let tareas = localStorage.getItem('tareas')
    if (tareas) {
      this.tareas = JSON.parse(tareas)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
