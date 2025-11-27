<template>
  <div>
    <h2>Lista de Tareas</h2>

    <!-- Formulario para añadir tareas -->
    <form @submit.prevent="agregarTarea">
      <input v-model="nuevaTarea" placeholder="Escribe una tarea" type="text" />
      <button type="submit">Agregar</button>
    </form>

    <!-- Tareas pendientes -->
    <h3>Pendientes</h3>
    <ul>
      <li v-for="tarea in pendientes" :key="tarea.id">
        {{ tarea.texto }}
        <div class="botones">
          <button @click="toggleCompletada(tarea)">✔️</button>
          <button @click="eliminarTarea(tarea)">🗑️</button>
        </div>
      </li>
    </ul>

    <!-- Tareas completadas -->
    <h3>Completadas</h3>
    <ul>
      <li v-for="tarea in completadas" :key="tarea.id">
        <span class="completada">{{ tarea.texto }}</span>
        <div class="botones">
          <button @click="toggleCompletada(tarea)">↩️</button>
          <button @click="eliminarTarea(tarea)">🗑️</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { computed, ref, watch } from 'vue'

// Generador de IDs únicos
const generarId = () => Date.now() + Math.random()

// Cargar tareas desde localStorage o usar iniciales
const tareasGuardadas = localStorage.getItem('tareas')
const tareas = ref(
  tareasGuardadas
    ? JSON.parse(tareasGuardadas)
    : [
        { id: generarId(), texto: 'Aprender vue', completada: false },
        { id: generarId(), texto: 'Aprender a hacer un Crud', completada: false },
        { id: generarId(), texto: 'Hacer correo o notificaciones en mi crud', completada: false }
      ]
)

const nuevaTarea = ref('')

// Añadir tarea
const agregarTarea = () => {
  const texto = nuevaTarea.value.trim()
  if (!texto) return
  tareas.value.push({ id: generarId(), texto, completada: false })
  nuevaTarea.value = ''
}

// Eliminar tarea
const eliminarTarea = (tarea) => {
  tareas.value = tareas.value.filter((t) => t.id !== tarea.id)
}

// Alternar estado completada
const toggleCompletada = (tarea) => {
  tarea.completada = !tarea.completada
}

// Computed para separar listas
const pendientes = computed(() => tareas.value.filter((t) => !t.completada))
const completadas = computed(() => tareas.value.filter((t) => t.completada))

// Persistir en localStorage
watch(
  tareas,
  (nuevas) => {
    localStorage.setItem('tareas', JSON.stringify(nuevas))
  },
  { deep: true }
)
</script>

<style scoped>
form {
  display: flex;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
}

input {
  flex: 1;
  padding: 0.6rem;
  border: 1px solid #42b883;
  border-radius: 6px;
  background: #000;
  color: #fff;
}

button {
  background: #feffff;
  color: #000;
  border: none;
  padding: 0.6rem 1rem;
  border-radius: 6px;
  cursor: pointer;
}

ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

li {
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #222;
  margin: 0.5rem 0;
  padding: 0.8rem;
  border-radius: 8px;
  color: #fff;
}
.botones{
    display: flex;
    gap: 1rem;

}
.completada {
  text-decoration: line-through;
  color: #bbb;
}
</style>
