<!--/////////////////////////////////////////////
//                                             //
// Edit & Design by White Bear (@howaitokuma). //
// Raihan Hafiizh Qurratu'Ain                  //
//                                             //
///////////////////////////////////////////////// -->
<template>
  <div>
    <input type="text" class="todo-input" placeholder="Ketik disini" v-model="newTodo" @keyup.enter="addTodo">
    <h3 class="List">List</h3>
    <transition-group name="fade" enter-active-class="animated fadeInUp" leave-active-class="animated fadeOutDown">
    <todo-item v-for="(todo, index) in todosFiltered" :key="todo.id" :todo="todo" :index="index" :checkAll="!anyRemaining" @removedTodo="removeTodo" @finishedEdit="finishedEdit">
      <!-- <div class="todo-item-left">
        <input type="checkbox" v-model="todo.completed">
        <div v-if="!todo.editing" @dblclick ="editTodo(todo)" class = "todo-item-label" :class="{ completed : todo.completed }">{{ todo.title }}</div>
        <input v-else class="todo-item-edit" type="text" v-model="todo.title" @blur="doneEdit(todo)" @keyup.enter="doneEdit(todo)" @keyup.esc="cancelEdit(todo)" v-focus>
      </div>
      <button type="button" class="btn btn-light" @click="removeTodo(index)">
        <i class="fas fa-times">&times;</i>
      </button> -->
    </todo-item>
    </transition-group>

  <div class="extra-container">
    <div><label><input type="checkbox" :checked="!anyRemaining" @change="checkAllTodos">  Check All</label></div>
    <div>{{ remaining }} items left</div>
  </div>

  <div class="extra-container">
    <div>
      <button type="button" class="btn btn-outline-warning" :class="{ active: filter == 'all' }" @click="filter = 'all'">All</button>
      <button type="button" class="btn btn-outline-info" :class="{ active: filter == 'active' }" @click="filter = 'active'">Active</button>
      <button type="button" class="btn btn-outline-success" :class="{ active: filter == 'completed' }" @click="filter = 'completed'">Completed</button>
    </div>

    <div>
      <transition name="fade">
      <button type="button" class="btn btn-outline-dark" v-if="showClearCompletedButton" @click="clearCompleted"><i>Delete</i></button>
      </transition>
    </div>
  </div>
  </div>
</template>

<script>
  import TodoItem from './TodoItem'

  export default {
    name: 'todo-list',
    components: {
      TodoItem,
    },
    data () {
      return{
        newTodo: '',
        idForTodo: 3,
        beforeEditChace: '',
        filter: 'all',
        todos: [
        {
          'id': 1,
          'title': 'Teh Manis',
          'completed': false,
          'editing' : false,
        },
        {
          'id': 2,
          'title': 'Es Teh Manis',
          'completed': false,
          'editing' : false,
        },
        
        ]
      }
    },

    computed:{
      remaining(){
        return this.todos.filter(todo => !todo.completed).length
      },
      anyRemaining(){
        return this.remaining != 0
      },
      todosFiltered(){
        if (this.filter == 'all'){
          return this.todos
        }else if(this.filter == 'active'){
          return this.todos.filter(todo => !todo.completed)
        }else if(this.filter == 'completed'){
          return this.todos.filter(todo => todo.completed)
        }

        return this.todos
      },
      showClearCompletedButton(){
        return this.todos.filter(todo => todo.completed).length > 0
      }
    },

    directives:{
      focus:{
        inserted: function(el){
          el.focus()
        }
      }
    },
    methods: {
      addTodo() {
        if(this.newTodo.trim().length == 0){
          return
        }

        this.todos.push({
          id: this.idForTodo,
          title: this.newTodo,
          completed: false,
        })

        this.newTodo = ''
        this.idForTodo++
      },
      
      editTodo(todo){
        this.beforeEditChace = todo.title
        todo.editing = true
      },

      doneEdit(todo){
        if(todo.title.trim() == ''){
          todo.title = this.beforeEditChace
        }
        todo.editing = false
      },
      cancelEdit(todo){
        todo.title = this.beforeEditChace
        todo.editing = false
      },

      removeTodo(index){
        this.todos.splice(index, 1)
      },
      checkAllTodos(){
        this.todos.forEach((todo) => todo.completed = event.target.checked)
      },
      clearCompleted(){
        this.todos = this.todos.filter(todo => !todo.completed)
      },
      finishedEdit(data){
        this.todos.splice(data.index, 1, data.todo)
      }
    }
  }
</script>

<style lang="scss">
  @import url(
    "https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.5.2/animate.min.css"
  );

  .todo-input {
    width: 100%;
    padding: 10px 18px;
    font-size: 18px;
    margin-bottom: 16px;

    &:focus {
      outline: 0;
    }
  }

  .todo-item{
    margin-bottom: 12px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    animation-duration: 0.3s;
  }
  .remove.item{
    cursor: pointer;
    margin-left: 14px;
    &:hover {
      color: black;
    }
  }

  .todo-item-left{
    display:flex;
    align-items: center;
  }

  .todo-item-label{
    padding: 10px;
    border: 1px solid white;
    margin-left: 12px;
  }

  .todo-item-edit{
    font-size: 24px;
    color: #2c3e50;
    margin-left: 12px;
    width: 100%;
    padding: 10px;
    border: 1px solid #ccc;
    font-family: 'avenir', Helvetica, Arial, sans-serif;
  }

  .completed {
    text-decoration: line-through;
    color: grey;
  }

  .extra-container{
    display: flex;
    align-items: center;
    justify-content: space-between;
    font-size: 16px;
    border-top: 1px solid lightgrey;
    padding-top: 14px;
    margin-top: 14px;
  }

  button {
    font-size: 14px;
    background-color: white;
    appearance: none;

    &:hover{
      background: lightgreen;
    }

    &:focus {
      outline: none;
    }
  }

  .List{
    font-family: 'Arial';
    text-align: left;
    }

  .btn{
    margin-left: 5px;
  }

  //transitions
  .fade-enter-active, .fade-leave-active{
    transition: opacity .2;
  }

  .fade-enter, .fade-leave-to{
    opacity: 0;
  }
  
</style>