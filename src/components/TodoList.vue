<template>
    <div id="app">
      <h2>Список задач</h2>
      <input v-model="newTodo" placeholder="Добавить новую задачу">
      <button class="create-btn" @click="addTodo">Создать</button>
      <ul>
        <li v-for="(todo, index) in todos" :key="index" class="todo-item">
          <span :class="{ 'selected': index === selectedTask }">{{ todo }}</span>
          <button @click="deleteTodo(index)" class="delete-btn">Удалить</button>
          <button @click="showUpdateModal(index)" class="update-btn">Изменить</button>
        </li>
      </ul>
  
      <div v-if="showModal" class="modal">
        <div class="modal-content">
          <span class="close" @click="hideModal">&times;</span>
          <input v-model="newValue" placeholder="Новое значение" @keyup.enter="updateTodo">
          <button @click="updateTodo" class="save-btn">Сохранить</button>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'TodoList',
    data() {
      return {
        todos: [],
        newTodo: '',
        selectedTask: null,
        newValue: '',
        showModal: false
      }
    },
    methods: {
      addTodo() {
        if (this.newTodo.trim() !== '') {
          this.todos.push(this.newTodo);
          this.newTodo = '';
        }
      },
      deleteTodo(index) {
        this.todos.splice(index, 1);
      },
      showUpdateModal(index) {
        this.selectedTask = index;
        this.newValue = this.todos[index];
        this.showModal = true;
      },
      hideModal() {
        this.selectedTask = null;
        this.newValue = '';
        this.showModal = false;
      },
      updateTodo() {
        if (this.newValue.trim() !== '') {
          this.todos[this.selectedTask] = this.newValue;
          this.hideModal();
        }
      }
    }
  }
  </script>
  
  <style>
  .todo-item {
    display: flex;
    align-items: center;
    margin-bottom: 10px;
    justify-content: center;
    position: relative;
    left: -34px;
  }
  
  .delete-btn {
    margin-left: 10px;
    background-color: #ff5a5a;
    color: #fff;
    border: none;
    padding: 5px 10px;
    border-radius: 5px;
    cursor: pointer;
  }
  
  .delete-btn:hover {
    background-color: #ff3d3d;
  }
  
  .update-btn {
    margin-left: 10px;
    background-color: #0099ff;
    color: #fff;
    border: none;
    padding: 5px 10px;
    border-radius: 5px;
    cursor: pointer;
  }
  
  .create-btn {
    margin-left: 10px;
    background-color: green;
    color: #fff;
    border: none;
    padding: 5px 10px;
    border-radius: 5px;
    cursor: pointer;
  }
  
  .update-btn:hover {
    background-color: #007acc;
  }
  
  .selected {
    font-weight: bold;
  }
  
  .modal {
    display: block;
    position: fixed;
    z-index: 1;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    overflow: auto;
    background-color: rgba(0, 0, 0, 0.4);
  }
  
  .modal-content {
    background-color: #fefefe;
    margin: 15% auto;
    padding: 20px;
    border: 1px solid #888;
    width: 300px;
  }
  
  .save-btn {
    margin-left: 10px;
    background-color: #6fd056;
    color: #fff;
    border: none;
    padding: 5px 10px;
    border-radius: 5px;
    cursor: pointer;
  }
  
  .save-btn:hover {
    background-color: #5aa646;
  }

  .close{
    position: relative;
    left: 289px;
    bottom: 16px;
    color: red;
    cursor: pointer;
  }

  </style>