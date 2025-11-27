<template>
  <div>
    <h2>Bienenido a tu app de Tareas</h2>
    <p>Organiza tus pendientes y mantente productivo</p>
    <RouterLink to="/tareas">
      <button>Ir a la lista de Tareas</button>
    </RouterLink>
  </div>
</template>


<style scoped>
h2 {
  color: var(--accent);
  margin-bottom: 1rem;
}
button {
  background: var(--accent);
  color: var(--accent-contrast);
  padding: 0.6rem 1rem;
  border: none;
  border-radius: 8px;
  cursor: pointer;
}
</style>
