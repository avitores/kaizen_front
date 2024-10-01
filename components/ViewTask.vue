<template lang="pug">
div.container
	if (error)
		p Error: {{ error }} <!-- Muestra error si ocurre -->
	else
		h1 {{ task.title }}
		p {{ task.description }}
		button(@click="$emit('edit-task', task.id)") Edit Task
		button(@click="$emit('delete-task', task.id)") Delete Task
</template>

<script>
export default {
  data() {
    return {
      task: {},
      id: this.$route.params.id, // Obtiene el ID de la tarea desde la ruta
      error: null, // Variable para almacenar posibles errores
    }
  },
  async mounted() {
    try {
      this.task = await this.$axios.$get(
        `http://localhost:3000/api/v1/tasks/${this.id}`
      ) // Cambia a tu API
    } catch (error) {
      console.error('Error fetching task:', error)
      this.error = error.message // Manejo de errores
    }
  },
}
</script>
