<template lang="pug">
div(class="container")
	h1 
		| Listado de Tasks
	h2
		| {{ tasks.length }} task{{ (tasks.length && tasks.length > 1)? 's' : '' }} encontrada{{ (tasks.length && tasks.length > 1)? 's' : '' }}
	p
		button(@click="createTask") Create New Task
	table
		tr(v-for="task in tasks" :key="task.id" class="m-2")
			td
				| {{ task.title }}
				td
				| {{ task.description }}
			td
				button(@click="viewTask(task.id)") View
				button(@click="editTask(task.id)") Edit
				button(@click="deleteTask(task.id)") Delete
</template>

<script>
export default {
  data() {
    console.log('OJO! Ha entrado en data')
    return {
      tasks: [],
    }
  },
  async mounted() {
    console.log('OJO! Ha entrado en async')
    try {
      const response = await this.$axios.get('/api/v1/tasks')
      console.log('Response Status:', response.status) // Muestra el código de estado
      console.log('Response Data:', response.data) // Muestra los datos de la respuesta
      this.tasks = response.data
      return { tasks: response.data }
    } catch (error) {
      console.error('Error fetching tasks:', error)
      return { tasks: [], error: error.message }
    }
  },

  methods: {
    viewTask(id) {
      this.$router.push(`/tasks/${id}`)
    },
    editTask(id) {
      this.$router.push(`/tasks/edit/${id}`)
    },
    createTask() {
      this.$router.push('/tasks/new')
    },
    async deleteTask(id) {
      await this.$axios.$delete(`/api/v1/tasks/${id}`)
      this.tasks = this.tasks.filter((task) => task.id !== id)
    },
  },
}
</script>
