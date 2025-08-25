<script setup>
  import './index.css'  
  import Task from './components/Task.vue'
  import NewTaskForm from './components/NewTaskFrom.vue'
</script>

<script>
export default {
  data() {
    return {
      tasks: [],
      id: 0,
      creatingTask: true
    }
  },
  methods: {
    addTask(taskData) {
      this.tasks.push({
        id: Date.now(),
        title: taskData.title,
        description: taskData.description,
        done: false
      })
      this.creatingTask = false
    },
    deleteTask(id){
      this.tasks = this.tasks.filter(task => task.id !== id);
    },
    toggleTask(id) {
      const task = this.tasks.find(t => t.id === id)
      if (task) task.done = !task.done
    }
  }
}
</script>

<template>
  <header>
    <h1>ToDo List App</h1>
  </header>

  <div class="general-tasks-container">
    <div class="add-task">
      <button class = "add-task-btn" @click="creatingTask = true">
        <div class="add-icon"></div>
        <span>Add Task</span>
      </button>
    </div>
    
    <NewTaskForm v-if="creatingTask" @confirm-task="addTask" @cancel-task="creatingTask = false"/>

    <div class="tasks-container">
      <Task v-for="task in tasks" :key="task.id" :task="task" @delete-task="deleteTask" @toggle-task="toggleTask"/>
    </div>
  </div>

  <main>
  </main>
</template>
