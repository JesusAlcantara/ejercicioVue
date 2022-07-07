<template>

  <h1 class="my-5">Formularios con Vue.js</h1>

  <form @submit.prevent="procesarFormulario()">
    <Input :tarea="tarea"/>
  </form>
  <hr>
  <ListaTareas />
</template>

<script>

import { mapActions } from 'vuex'
import Input from '../components/Input'
import ListaTareas from '../components/ListaTareas'
const shortid = require('shortid')

export default {
  name: 'HomeView',
  components: {
    Input,
    ListaTareas
  },
  data() {
    return {
      tarea: {
        id: '',
        nombre: '',
        categorias: [],
        estado: '',
        numero: 0
      }
    }
  },
  methods: {
    ...mapActions(['setTareas']),
    procesarFormulario() {
      console.log(this.tarea)
      if(this.tarea.nombre.trim() == "") {
        console.log("Campo vacío")
        return
      }
      console.log("No está Vacío")

      // Genera ID aleatorio
      this.tarea.id = shortid.generate()

      // Enviar datos
      this.setTareas(this.tarea)

      // Limpiar datos al procesar
      this.tarea = {
        id: '',
        nombre: '',
        categorias: [],
        estado: '',
        numero: 0
      }
    }
  }
}
</script>
