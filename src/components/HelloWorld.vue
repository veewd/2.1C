<template>
  <div class="todo-app">
    <h1>Todo App</h1>
    <h2>My Tasks</h2> <!-- Added heading for "My Tasks" -->
    <input v-model="newTask" @keyup.enter="addTask" placeholder="Enter a new task">
    
    <button @click="toggleCompletedTasks">{{ showCompleted ? 'Hide Completed Tasks' : 'Show Completed Tasks' }}</button>
    
    <ul>
      <li v-for="(task, index) in filteredTasks" :key="index" v-show="showTask(task)">
        <input type="checkbox" v-model="task.completed">
        <span :class="{ completed: task.completed }">{{ task.text }}</span>
        <button @click="removeTask(index)">Remove</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: [],
      showCompleted: true
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== '') {
        this.tasks.push({
          text: this.newTask,
          completed: false
        });
        this.newTask = '';
      }
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    },
    toggleCompletedTasks() {
      this.showCompleted = !this.showCompleted;
    },
    showTask(task) {
      return this.showCompleted || !task.completed;
    }
  },
  computed: {
    filteredTasks() {
      return this.tasks.filter(task => this.showTask(task));
    }
  }
};
</script>

<style scoped>
.todo-app {
  max-width: 400px;
  margin: 0 auto;
  text-align: center;
  font-family: Arial, sans-serif;
  background-color: #f4f4f4;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
}

h1 {
  color: #333;
}

input {
  padding: 10px;
  font-size: 16px;
  width: 100%;
  margin-bottom: 10px;
}

button {
  padding: 10px 20px;
  background-color: #f44336;
  border: none;
  color: white;
  cursor: pointer;
  border-radius: 5px;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #d32f2f;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  display: flex;
  align-items: center;
  margin: 10px 0;
  background-color: white;
  padding: 10px;
  border-radius: 5px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
}

li:hover {
  transform: scale(1.02);
}

.completed {
  text-decoration: line-through;
  color: #888;
}

</style>
