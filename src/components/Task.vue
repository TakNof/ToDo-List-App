<script scoped>
    import '../Task.css'

export default {
  props: {
    task: {
      type: Object,
      required: true
    }
  },
  methods: {
    deleteTask() {
      this.$emit('delete-task', this.task.id)
    }
  }
}
</script>

<template>
    <div class="task-card":class="task.done ? 'task-done' : 'task-pending'">
        <h2 class="card-title">{{task.title}}</h2>
        <p class="card-desc">{{ task.description }}</p>
        <div class="task-status">
            <input type="checkbox" :checked="task.done" @change= "$emit('toggle-task', task.id)" />
            <button @click="deleteTask">Delete</button>
        </div>
    </div>  
</template>