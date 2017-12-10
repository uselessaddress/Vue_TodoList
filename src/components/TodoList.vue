<template>
  <div>
      <input 
        v-model="newTodoText"
        placeholder="New Todo"
        @keydown.enter="addTodo"
        >
        <ul v-if="todos.length">
            <TodoListItem 
                v-for="todo in todos"
                :key="todo.id"
                :todo="todo"
                @remove="removeTodo" 
            >
            </TodoListItem>    
        </ul>
  </div>
</template>
<script>
import TodoListItem from './TodoListItem.vue'
let nextTodoId = 1
export default {
   components: {
       TodoListItem
   },
   data(){
       return {
           newTodoText: '',
           todos: [
                {
                   id: nextTodoId++,
                   text: 'learn vue'
                },
                {
                   id: nextTodoId++,
                   text: 'Learn about single-file components'
                },
                {
                   id: nextTodoId++,
                   text: 'fall in love'
                },
           ]
       }
   },
   methods: {
       addTodo(){
           const trimmedText = this.newTodoText.trim()
           if(trimmedText){
               this.todos.push({
                   id:nextTodoId++,
                   text:trimmedText
               })
               this.newTodoText = ''
           }
       },
       removeTodo(idToRemove){
           this.todos = this.todos.filter(todo=>{
               return todo.id !== idToRemove
           })
       }
   }
}
</script>
