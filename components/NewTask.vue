<template lang="pug">
div.container
	h1 Create a New Task
	form(@submit.prevent="createTask")
		div.form-group
			label(for="title") Title:
			input(type="text" v-model="task.title" required placeholder="Enter task title" id="title")

		div.form-group
			label(for="description") Description:
			textarea(v-model="task.description" required placeholder="Enter task description" id="description")

		button(type="submit") Create Task
		p(v-if="error") Error: {{ error }} <!-- Muestra error si ocurre -->
</template>

<script>
export default {
  data() {
    return {
      task: {
        title: '',
        description: '',
      },
      error: null, // Variable para almacenar posibles errores
    }
  },
  methods: {
    async createTask() {
      try {
        await this.$axios.$post('/api/v1/tasks', this.task) // Cambia a tu API
        this.$router.push('/tasks') // Redirige a la lista de tareas después de crear
      } catch (error) {
        console.error('Error creating task:', error)
        this.error = error.message // Manejo de errores
      }
    },
  },
}
</script>
