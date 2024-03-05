<template>
  <main>
    <!-- heading -->
    <header>
      <img src="./assets/pinia-logo.svg" alt="pinia logo">
      <h1>
        Pinia Tasks
      </h1>
    </header>

    <!-- new task form -->
    <div class="new-task-form">
      <TaskForm />
    </div>
    <!-- filter -->
    <nav class="filter">
      <button @click="filter = 'all'">
        All Tasks
      </button>
      <button @click="filter = 'favs'">
        Favs Tasks
      </button>
    </nav>
    <!-- loading -->
    <div class="loading" v-if="taskStore.loading">Loading tasks</div>
    <!-- tasks lists -->
    <div class="task-list" v-if="filter === 'all'">
      <p>You have {{ taskStore.totalCount  }} tasks left to do</p>
      <div
        v-for="task in taskStore.tasks"
        :key="task.id">
          <TaskDetails :task="task"/>
      </div>
    </div>
    <div class="task-list" v-if="filter === 'favs'">
      <p>You have {{ taskStore.favCount  }} favs left to do</p>
      <div
        v-for="task in taskStore.favs"
        :key="task.id">
          <TaskDetails :task="task"/>
      </div>
    </div>
    <button @click="taskStore.$reset">Reset State</button>
  </main>
</template>

<script>
import { ref } from 'vue';
import TaskDetails from './components/TaskDetails.vue';
import { useTaskStore } from './stores/TaskStore';
import TaskForm from './components/TaskForm.vue';
// import { storeToRefs } from 'pinia';
export default {
  components: { TaskDetails, TaskForm },
  setup() {
    const taskStore = useTaskStore()
    // const { tasks, loading, favs, totalCount, favCount} = storeToRefs(taskStore)
    //fetch tasks
    taskStore.getTasks()
    const filter = ref('all')
    return {
      taskStore,
      filter
    }
  }
}
</script>