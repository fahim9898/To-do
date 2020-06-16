<template>

  <div id="app" class="container">
    <br>
    <h1 class="text-center">Todo App</h1>

    <form @submit.prevent="addTodo">
      <div class="form-group">
        <label for="Add-ittem-label">Add Things To Do</label>
        <input v-model="newTodo" autocomplete="off" type="text" class="form-control" id="enter_todo" aria-describedby="emailHelp">
       </div> 
       <button type="submit" class="btn btn-info">Add Items</button>
    </form>
    <br>
    <ul>
      <li v-for="todo of todo_list">
        <div class="input-group mb-3">
          <div class="input-group-prepend">
            <div class="input-group-text">
              <input type="checkbox" v-model="todo.done">
            </div>
          </div>
          <p id = "todo-text" class="form-control text-center font-weight-bold" @click="check_on_click(todo)" v-bind:class="{checked_done : todo.done}">{{todo.message}}</p>
          <button @click="removeItem(todo)" type="button" class="btn btn-danger">Remove</button>
        </div>
      </li>  
    </ul>

  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      newTodo: "", 
      todo_list:[]
    }
  },
  mounted(){
      if(localStorage.todos){
        this.todo_list = JSON.parse(localStorage.todos)
      }
      
  },
  watch:{
      todo_list : {
        handler(){
          localStorage.todos = JSON.stringify(this.todo_list)
        },
        deep: true
      }
    },
  methods :{
    addTodo(){
      if(this.newTodo != ""){
        this.todo_list.push({done:false , message:this.newTodo})
        this.newTodo=""
      }
    },

    check_on_click(todo){
      todo.done = !todo.done
    },

    removeItem(todo){
        // console.log()
        // console.log(todo_list)
        let index_item = this.todo_list.indexOf(todo)
        console.log(index_item)
        this.todo_list.splice(index_item , 1)
    }

  }
}
</script>

<style>
  ul{
    list-style-type:none;
  }

  .checked_done{
    text-decoration: line-through;
  }

  #todo-text{
    cursor: pointer;
  }
</style>