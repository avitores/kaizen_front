<template lang="pug">
div.container
  h1 Edit Task
  form(@submit.prevent="updateTask")
    div.form-group
      label(for="title") Title:
      input(type="text" v-model="task.title" required placeholder="Enter task title" id="title")

    div.form-group
      label(for="description") Description:
      textarea(v-model="task.description" required placeholder="Enter task description" id="description")

    button(type="submit") Update Task
    p(v-if="error") Error: {{ error }}
</template>

<script>
export default {
  data() {
    return {
      task: {
        title: '',
        description: '',
      },
      error: null,
    }
  },
  async mounted() {
    await this.fetchTask() // Llama a la función para obtener la tarea al montar el componente
  },
  methods: {
    async fetchTask() {
      try {
        const id = this.$route.params.id // Obtiene el ID de la tarea desde la ruta
        this.task = await this.$axios.$get(`/api/v1/tasks/${id}`) // Llama a la API para obtener la tarea
      } catch (error) {
        console.error('Error fetching task:', error)
        this.error = error.message // Manejo de errores
      }
    },
    async updateTask() {
      try {
        const id = this.$route.params.id // Obtiene el ID de la tarea desde la ruta
        await this.$axios.$put(`/api/v1/tasks/${id}`, this.task) // Llama a la API para actualizar la tarea
        this.$router.push('/tasks') // Redirige a la lista de tareas
      } catch (error) {
        console.error('Error updating task:', error)
        this.error = error.message // Manejo de errores
      }
    },
  },
}
</script>
