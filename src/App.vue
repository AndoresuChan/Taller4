<template>
  <div class="todo-list">

    <h1>{{ listaNombre }}</h1>

    <input class="list-name" v-model="listaNombre" @blur="guardarNombre" placeholder="Nombre de lista">
    
    <form @submit.prevent="agregarTarea" class="add-task-form">

      <input class="new-task-input" v-model="nuevaTarea" placeholder="Nueva tarea">

      <button type="submit" class="add-task-btn">Agregar</button>

    </form>

    <ul class="tasks-list">


      <li v-for="(tarea, index) in tareas" :key="index" class="task-item">
        <input class="task-input" v-model="tareas[index]" @keyup.enter="guardarEdicion(index)" @blur="guardarEdicion(index)">
        
        <button @click="eliminarTarea(index)" class="delete-task-btn">Eliminar</button>

      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      listaNombre: 'Lista',
      nuevaTarea: '',
      tareas: ['Tarea Ejemplo']
    };
  },
  methods: {
    guardarNombre() {
      if (this.listaNombre.trim() === '') {
        this.listaNombre = 'Lista'; // Si el nombre está vacío, restauramos el nombre por defecto
      }
    },
    agregarTarea() {
      if (this.nuevaTarea.trim() !== '') {
        this.tareas.push(this.nuevaTarea);
        this.nuevaTarea = '';
      }
    },
    eliminarTarea(index) {
      this.tareas.splice(index, 1);
    },
    guardarEdicion(index) {
      if (this.tareas[index].trim() === '') {
        this.tareas.splice(index, 1); // Eliminar la tarea si está vacía
      }
    }
  }
};
</script>

<style scoped>
.todo-list {
  max-width: 400px;
  margin: auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.list-name {
  margin-bottom: 10px;
  width: 100%;
  padding: 5px;
}

.add-task-form {
  display: flex;
  margin-bottom: 10px;
}

.new-task-input {
  flex: 1;
  padding: 5px;
  border-radius: 5px;
}

.add-task-btn {
  padding: 5px 10px;
  border: none;
  border-radius: 5px;
  background-color: #007bff;
  color: #fff;
  cursor: pointer;
}

.tasks-list {
  list-style: none;
  padding: 0;
}

.task-item {
  display: flex;
  align-items: center;
  margin-bottom: 5px;
}

.task-input {
  flex: 1;
  padding: 5px;
  border-radius: 5px;
}

.delete-task-btn {
  margin-left: 5px;
  padding: 5px 10px;
  border: none;
  border-radius: 5px;
  background-color: #dc3545;
  color: #fff;
  cursor: pointer;
}
</style>
