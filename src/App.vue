<template>
  <div class="is-flex-direction-column">
    <img @click="changeTheme()" class="imgLogo" alt="Vue logo" src="./assets/note.png">
    <FormInput @add="addTodo"/> 
    <br>
    <h5 class="title is-5" v-show="todos.length > 0">SUAS TAREFAS</h5>
    <h5 class="title is-5" v-show="todos.length == 0">NÃO HÁ TAREFAS</h5>
 <ModalConfirm 
  :class="modalTrigger" 
  @cancel="cancel" 
  @confirm="deleteTodo(canceledIndex)"
  /> 
    <div v-for="(todo,index) in todos" :key="index"> 
      <Todo :selected="(index)" @edit="editTodo" @remove="toggleModal(index)" :msg="todos[index]"/> 
    </div>
  </div>
</template>

<script>
import Todo from './components/To-do.vue';
import FormInput from './components/Form-input.vue';
import ModalConfirm from './components/Modal-confirm.vue';

export default {
  name: 'App',
  components: {
    Todo,
    FormInput,
    ModalConfirm
},
  data(){
    return {
      todos: [],
      modalTrigger: '',
      canceledIndex: null
    }
  },
  created(){
    if(localStorage.tasks){
      this.todos = JSON.parse(localStorage.tasks);
    }
    else{
      this.todos = [];
    }
  },
  methods: {
    addTodo(task) {
      if(task){
        this.todos.push(task);
        localStorage.tasks = JSON.stringify(this.todos);
      }
    },
    toggleModal(index){
      this.modalTrigger = "is-active";  
      this.canceledIndex = index;
    },
    cancel(){
       this.modalTrigger=''
    },
    deleteTodo(index){
      this.todos.splice(index, 1);
      localStorage.tasks = JSON.stringify(this.todos);
    },
    editTodo(newTodo, selectedIndex){
      this.todos[selectedIndex] = newTodo;
      localStorage.tasks = JSON.stringify(this.todos);
    },
    changeTheme(){
      const root = document.getElementById('html-root');
      if(root.classList.contains('black')){
        root.classList.remove('black')
      }
      else{
        root.classList.add('black');
      }
     
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 20px;
}
.imgLogo{
  max-width: 5rem;
  margin-bottom: 10px;
}
.imgLogo:hover{
  cursor: pointer;
  transform: scale(0.9);
}
.black{
  background-color:hsl(0, 0%, 7%);
}
.title{
  color: hsl(0, 0%, 29%);
}
</style>
