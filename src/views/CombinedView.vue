<template>
    <div class="container mt-4">
        <h1 class="text-center text-acuamarine mb-4">Lista de Tareas</h1>
        <div class="input-group mb-3">
            <input v-model="newTask" @keyup.enter="addTask" placeholder="Añadir nueva tarea"
                class="form-control task-input" aria-label="Nueva tarea" />
            <button @click="addTask" class="btn btn-acuamarine">Añadir</button>
        </div>
        <div class="row mt-4">
            <div class="col-12 mb-4" v-for="task in tasks" :key="task.id">
                <div class="card mb-3">
                    <div class="card-body d-flex justify-content-between align-items-center">
                        <div class="flex-grow-1 me-2">
                            <h5 class="card-title m-0" :class="{ 'text-decoration-line-through': task.completed }">
                                {{ task.todo }}
                            </h5>
                            <span class="badge"
                                :class="{ 'bg-success': task.completed, 'bg-warning': !task.completed }">
                                {{ task.completed ? 'Completada' : 'Pendiente' }}
                            </span>
                        </div>
                        <div class="d-flex">
                            <button @click="toggleTaskCompletion(task)" class="btn btn-outline-success me-2"
                                aria-label="Marcar como completada">
                                <i :class="task.completed ? 'bi bi-check-circle-fill' : 'bi bi-check-circle'"></i>
                            </button>
                            <button @click="deleteTask(task.id)" class="btn btn-outline-danger"
                                aria-label="Eliminar tarea">
                                <i class="bi bi-trash"></i>
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
  export default {
    name: "CombinedView",
    props: ['tasks'],
    data() {
      return {
        newTask: "",
      };
    },
    methods: {
      addTask() {
        if (this.newTask.trim() === "") return;

        const newTask = {
          todo: this.newTask,
          completed: false,
          id: Date.now(), 
        };

        this.$emit('add-task', newTask); 
        this.newTask = "";
      },
      toggleTaskCompletion(task) {
        task.completed = !task.completed; 
      },
      deleteTask(taskId) {
        this.$emit('delete-task', taskId); 
      },
    },
  };
  </script>

<style scoped>
.container {
    max-width: 800px;
    padding: 20px;
    background-color: #e0f7f9;
    border-radius: 10px;
}

h1 {
    font-size: 2.5rem;
    font-weight: bold;
    text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.3);
    color: aquamarine;
}

.task-input {
    border-radius: 25px;
    transition: border-color 0.2s;
}

.task-input:focus {
    outline: none;
    box-shadow: 0 0 5px rgba(0, 123, 255, 0.5);
}

.card {
    border: 1px solid aquamarine;
    background-color: #f0ffff;
}

.card-title {
    font-weight: bold;
    overflow-wrap: break-word;
    max-height: 3em;
    overflow: hidden;
}

.text-decoration-line-through {
    text-decoration: line-through;
}

.badge {
    font-weight: bold;
}

.btn-acuamarine {
    background-color: aquamarine;
    color: white;
}

.btn-outline-success {
    color: aquamarine;
    border-color: aquamarine;
}

.btn-outline-success:hover {
    background-color: aquamarine;
    color: white;
}

.btn-outline-danger {
    color: #dc3545;
    border-color: #dc3545;
}

.btn-outline-danger:hover {
    background-color: #dc3545;
    color: white;
}
</style>

