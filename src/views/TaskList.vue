<template>
    <div class="container mt-4">
        <h1 class="text-center title">Lista de Tareas</h1>
        <button @click="fetchTasks" class="btn btn-acuamarine mb-3">
            <i class="bi bi-arrow-clockwise me-2"></i>Cargar Tareas
        </button>
        <div v-if = "showTasks" class="row">
            <div class="col-12 mb-4" v-for="task in tasks" :key="task.id">
                <TodoItem :title="task.todo" :completed="task.completed" 
                    @toggle-completion="toggleTaskCompletion(task)"
                    @delTodo="deleteTask(task.id)" />
            </div>
        </div>
    </div>
</template>

<script>
import TodoItem from "@/components/TodoItem.vue";
import axios from "axios"; 

export default {
    props: ['tasks'], 
    components: { TodoItem },
    data() {
        return {
            showTasks: false, 
        };
    },
    methods: {

        fetchTasks() {
            axios
                .get("https://dummyjson.com/todos")
                .then((response) => {
                    this.$emit('update:tasks', response.data.todos); 
                    this.showTasks = true; 
                })
                .catch((error) => {
                    console.error("Error fetching tasks:", error);
                });
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
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
}
.title {
    color: aquamarine;
    font-size: 2.5rem;
    font-weight: bold;
    text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.3);
}
.btn-acuamarine {
    background-color: aquamarine;
    color: white;
    border: none;
    transition: background-color 0.3s;
}
.btn-acuamarine:hover {
    background-color: #1a8b83;
}
.todo-item {
    background-color: #f0ffff;
    border-radius: 8px;
    padding: 15px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}
</style>