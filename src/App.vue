<template>
  <Layout>
    <div class="composer">
      <Form v-model="newTodo" @submitTodo="addTodo" :isError="isError"/>
      <Filter 
        :selectedFilter="selectedFilter" 
        @filterAll="selectedFilter = 'all'" 
        @filterPending="selectedFilter = 'pending'" 
        @filterDone="selectedFilter = 'done'"
        :total="totalTodos" 
        :pending="pendingTodos" 
        :done="doneTodos"
        @clear="clearDoneTodo"
      />
    </div>

    <Todo v-for="todo in filteredTodos" :key="todo.id" :todo="todo" @toggleTodo="toggleTodo(todo)"/>
  </Layout>
</template>

<script>
import {v4 as uid} from "uuid";
import Layout from './components/Layout.vue';
import Todo from './components/Todo.vue';
import Form from './components/Form.vue';
import Filter from './components/Filter.vue';

export default {
  name: "TodoApp",
  components: {
    Layout,
    Todo,
    Form,
    Filter
  },
  data(){
    return{
      todos: [],
      newTodo: "",
      selectedFilter: "all",
      isError: false,
    }
  },
  mounted(){
    this.todos = JSON.parse(localStorage.getItem("todos"));
  },
  watch: {
    todos:{
      handler(newValue){
        localStorage.setItem("todos", JSON.stringify(this.todos))
      },
      deep: true
    },
    newTodo(newValue){
      if(newValue != ''){
        this.isError = false;
      }
    }
  },
  computed: {
    totalTodos(){
      if(this.todos){
        return this.todos.length;
      }
    },
    pendingTodos(){
      if(this.todos){
        return this.todos.filter(todo => !todo.status).length;
      }
    },
    doneTodos(){
      if(this.todos){
        return this.todos.filter(todo => todo.status).length;
      }
    },
    filteredTodos(){
      if(this.selectedFilter == "all"){
        return this.todos;
      }else if(this.selectedFilter == "pending"){
        return this.todos.filter(todo => !todo.status);
      }else if(this.selectedFilter == "done"){
        return this.todos.filter(todo => todo.status);
      }
    }
  },
  methods: {
    addTodo(){
      if(this.newTodo == ''){
        this.isError = true;
      }else{
        let todo = {
          id: uid,
          title: this.newTodo,
          date: new Date().toString(),
          status: false,
        }
        this.todos.push(todo);
        this.newTodo = '';
        this.isError = false;
      }
    },
    toggleTodo(todo){
      todo.status = !todo.status;
    },
    clearDoneTodo(){
      this.todos = this.todos.filter(todo => !todo.status);
    },
    showDoneTodos(){
      this.filtered_todos = this.todos.filter(todo => todo.status);
    },
    showPendingTodos(){
      this.filtered_todos = this.todos.filter(todo => !todo.status);
    }
  }
}
</script>
