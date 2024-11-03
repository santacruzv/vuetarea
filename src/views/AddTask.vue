<template>
    <div class="container mt-4">
        <h1 class="text-center mb-4">Añadir Tarea</h1>
        <div class="input-group mb-3">
            <input v-model="newTask" @keyup.enter="addTask" placeholder="Añadir nueva tarea"
                class="form-control" />
            <button @click="addTask" class="btn btn-acuamarine">Añadir</button>
        </div>

        <div class="row mt-4" v-if="addedTasks.length > 0">
            <div class="col-12 mb-4" v-for="task in addedTasks" :key="task.id">
                <div class="card mb-3">
                    <div class="card-body d-flex justify-content-between align-items-center">
                        <div class="flex-grow-1 me-2">
                            <h5 class="card-title m-0" :class="{ 'text-decoration-line-through': task.completed }">
                                {{ task.todo }}
                            </h5>
                            <span class="badge"
                                :class="{ 'bg-acuamarine': task.completed, 'bg-warning': !task.completed }">
                                {{ task.completed ? 'Completada' : 'Pendiente' }}
                            </span>
                        </div>
                        <div class="d-flex">
                            <button @click="toggleTaskCompletion(task)" class="btn btn-outline-success me-2"
                                aria-label="Marcar como completada">
                                <i :class="task.completed ? 'bi bi-check-circle-fill' : 'bi bi-check-circle'"></i>
                            </button>
                            <button @click="deleteTask(task)" class="btn btn-outline-danger"
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
  props: ['tasks'], 
  data() {
    return {
      newTask: "",
      addedTasks: [], 
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

      this.addedTasks.push(newTask); 
      this.$emit('add-task', newTask); 
      this.newTask = ""; 
    },
    toggleTaskCompletion(task) {
      task.completed = !task.completed; 
    },
    deleteTask(task) {
      this.addedTasks = this.addedTasks.filter(t => t.id !== task.id); 
      this.$emit('delete-task', task.id); 
    },
  },
};
</script>

<style scoped>
.container {
    max-width: 800px;
    padding: 20px;
    background-color: #ecf2f3;
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
    background-color: #d4d6d5;
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
    color: rgb(191, 50, 50);
}

.btn-outline-success {
    color: aquamarine;
    border-color: aquamarine;
}

.btn-outline-success:hover {
    background-color: aquamarine;
    color: rgb(228, 223, 223);
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
