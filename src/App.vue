<template>
  <div id="app" class="container">
    <h1 class="text-center"> TODO APP</h1>
    <form @submit.prevent="addTodo()">
      <div class="form-group">
        <label for="newTodo">Add New Todo</label>
        <input v-model="newTodo" type="text" class="form-control" id="newTodo" aria-describedby="newTodoHelp" placeholder="Walk the dog.... ">
        <small id="emailHelp" class="form-text text-muted">Enter a New Todo</small>
      </div>
      <button type="submit" class="btn btn-primary">Submit</button>
    </form>

    <ul class="list-group">
      <li
      v-for="(todo, i) in todos" 
      class="list-group-item">
         <button 
         v-if="!todo.done"
         @click="taskDone(todo)" 
         type="button" 
         class="btn btn-success"> 
          DONE 
         </button>
         <button
         @click="deleteTask(i)"
         class="btn btn-danger"
         type="button">
           DELETE
         </button>
        <span 
        :class="{isDone: todo.done}"> 
        {{todo.title}}
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      newTodo: '',
      todos: []
    }
  },
  watch: {
    todos: {
      handler(){
        localStorage.todos = JSON.stringify(this.todos);
      },
      deep: true
    }
  },
  mounted(){
    if(localStorage.todos){
      this.todos = JSON.parse(localStorage.todos);
    }
  },
  methods: {
    addTodo(){
      this.todos.push({
        title: this.newTodo,
        done: false
      });
      this.newTodo
       = ' '
    },
    taskDone(todo){
      console.log(todo.title);
      todo.done = true
    },
    deleteTask(index){
      this.todos.splice(index, 1);
    }
  }
}
</script>

<style>
.list-group{
  margin-top: 25px;
}
.isDone{
  text-decoration: line-through;
}
</style>
