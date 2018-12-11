<template>
  <div id="app">
    <header class="header">
      <h3>Todos</h3>
      <input autofocus autocomplete="off" placeholder="Добавьте новый элемент" @keyup.enter="addTodo">    
    </header>
    <main>
      <ul>
        <TodoItem v-for="(todo, index) in filteredTodos" :key="index" :todo="todo"/> 
      </ul>
      <button @click="done = !done">{{ done ? 'Посмотреть новые' : 'Посмотреть исполненные' }}</button>  
    </main>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import { getModule } from 'vuex-module-decorators'
import TodoItem from '@/components/TodoItem.vue'
import { ITodo, ITodoGetter, IAddTodoAction } from './types'
import Todo  from './store/modules/todo'
const todoModule = getModule(Todo)
const commentCount = todoModule.filteredTodos(false)
@Component({
  components: { TodoItem } 
})
export default class App extends Vue {
  
  done: boolean = false
  get hotels() {
    return this.$store.state.todo.to
  }
  // get filteredTodos() {
  //   return this.$store.getters.filteredTodos(this.done)
  // }
   get filteredTodos() {
    return commentCount
  } 
  addTodo (e:any) {
    const text = e.target.value
    if (text.trim()) {
      this.$store.dispatch('addTodo', text)
    }
    e.target.value = ''
  }
}
</script>

<style>

</style>
