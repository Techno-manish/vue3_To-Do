<script setup>
  import { ref } from "vue"
  import { v4 as uuidv4 } from 'uuid';

  const inputText = ref("")
  let todoList = ref([])

  const defaultTodo = {
    id: uuidv4(),
    text: 'Please Enter Your todo here...'
  }

  todoList.value.push(defaultTodo)

  const addTodo = () => {
    if(inputText.value.length>5){
      const todo = {
        id: uuidv4(),
        text: inputText.value
      }
      todoList.value.push(todo)
      inputText.value = ""
    }else{
      alert("Your input is too short!!!...Enter a longer input.")
    }
  }

  const deleteTodo = (id) =>{
    todoList.value = todoList.value.filter(each=>each.id!==id)
    if(todoList.value.length===0){
      todoList.value.push(defaultTodo)
    }
  }

</script>

<template>
  <main>
    <div class="todo-container">
      <h1>This is a To-Do List</h1>
      <div class="inputContainer">
        <input type="text" class="inputBar" v-model="inputText" @keyup.enter="addTodo"/>
        <button class="addButton" @click="addTodo">Add To-Do</button>
      </div>
      <ul v-if="todoList.length>0"class="todo-list-container">
        <li v-for="todo in todoList" :key="todo.id" class="todo-list-item">
          <p class="todo-item">{{ todo.text }}</p>
          <button class="deleteButton" @click="deleteTodo(todo.id)">Delete</button>
        </li>
      </ul>
    </div>
  </main>
</template>

<style scoped>
  main {
    background-color: aliceblue;
    height: 100vh;
    width: 100vw;
    display: flex;
    justify-content: center;
  }

  .todo-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 80%;
    height: 90%;
  }

  .inputContainer {
    height: 4vh;
    background-color:rgb(174, 240, 240);
    display: flex;
    align-items: center;
    padding-left: 5px;
    border-radius: 10px;
  }

  .inputBar{
    width: 60vw;
    height: 3.5vh;
    margin-right: 5px;
    font-size: 16px;
    font-weight: bold;
    outline: none;
    border: none;
    background-color: transparent;
    text-align: center;
    color: rgb(45, 175, 207);
  }

  .addButton {
    height: 4vh;
    width: 8vw;
    border: none;
    font-size: 16px;
    background-color: blueviolet;
    color: rgb(174, 240, 240);
    font-weight: bold;
    cursor: pointer;
    border-top-right-radius: 10px;
    border-bottom-right-radius: 10px;
  }

  .todo-list-container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    background-color: rgb(211, 245, 245);
    width: 100%;
    margin-top: 3vh;
    padding-left: 0px;
  }

  .todo-list-item{
    width: 100%;
    height: 5vh;
    background-color: rgb(174, 240, 240);
    border: solid 2px rgb(166, 248, 248);
    display: flex;
    justify-content: space-between;
    align-items: center;
    list-style-type: none;
    margin-bottom: 5px;
  }
  .todo-item{
    font-size: large;
    font-weight: bold;
    padding: 0 0 0 2rem;
    color: rgb(45, 175, 207);
  }

  .deleteButton{
    height: 5vh;
    width: 8vh;
    font-size: 16px;
    font-weight: bold;
    padding-right: 0px;
    border: none;
    background-color: rgb(243, 72, 72);
    color: rgb(166, 248, 248);
    cursor: pointer;
  }
</style>