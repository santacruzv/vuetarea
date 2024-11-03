<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-dark bg-acuamarine shadow-sm">
      <div class="container">
        <router-link class="navbar-brand d-flex align-items-center" to="/">
          <img src="@/assets/logo.png" alt="Vue logo" width="30" height="30" class="d-inline-block align-top me-2" />
          Gestor de Tareas
        </router-link>

        <button
          type="button"
          @click="toggleNavbar"
          aria-controls="navbarNav"
          :aria-expanded="!isNavbarCollapsed"
          aria-label="Toggle navigation"
          class="navbar-toggler"
        >
          <span class="navbar-toggler-icon"></span>
        </button>

        <div :class="['collapse navbar-collapse', { show: !isNavbarCollapsed }]" id="navbarNav">
          <ul class="navbar-nav ms-auto">
            <li class="nav-item">
              <router-link class="nav-link d-flex align-items-center" to="/addtask">
                <i class="bi bi-plus-circle me-2"></i>Añadir Tarea
              </router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link d-flex align-items-center" to="/tasklist">
                <i class="bi bi-card-list me-2"></i>Lista de Tareas
              </router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link d-flex align-items-center" to="/combined">
                <i class="bi bi-grid me-2"></i>Vista Combinada
              </router-link>
            </li>
          </ul>
        </div>
      </div>
    </nav>
    <router-view :tasks="tasks" @add-task="addTask" @delete-task="deleteTask" />
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      isNavbarCollapsed: true,
      tasks: [],
    };
  },
  methods: {
    toggleNavbar() {
      this.isNavbarCollapsed = !this.isNavbarCollapsed;
    },
    addTask(newTask) {
      this.tasks.unshift(newTask); 
    },
    deleteTask(taskId) {
      this.tasks = this.tasks.filter(task => task.id !== taskId); 
    },
    fetchTasks() {
      axios
        .get("https://dummyjson.com/todos")
        .then((response) => {
          this.tasks = response.data.todos.map(task => ({
            ...task,
            completed: task.completed || false, 
          }));
        })
        .catch((error) => {
          console.error("Error fetching tasks:", error);
        });
    },
  },
  created() {
    this.fetchTasks();
  },
};
</script>


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}


.navbar {
  background-color: #20b2aa; 
  margin-bottom: 20px;
}

.navbar-brand,
.nav-link {
  color: #7fffd4; 
}

.nav-link {
  font-weight: bold;
  color: #7fffd4;
  transition: color 0.3s;
}

.nav-link:hover {
  color: #e0ffff; 
}

.nav-link.router-link-exact-active {
  color: #00ced1; 
  text-decoration: underline; 
}

.navbar-brand img {
  border-radius: 50%;
}

.container {
  max-width: 1100px;
}


body {
  background-color: #7fffd4; 
}
</style>
