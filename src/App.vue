<template>
  <div class="container" style="margin-top: 20px;">
    <div class="card">
      <div class="card-body">
        <h5 class="card-title">Simple TodoList App</h5>
        <small class="mt-3">Total Todo : {{ totalTODO }}</small>
        <div class="row">
          <div class="col-10">
            <input type="text" class="form-control " v-model="todo" @keyup.enter="add">
          </div>
          <div class="col-2">
            <button class="btn btn-outline-success" @click="add">Add</button>
          </div>
        </div>
        <!-- List Todolist -->
       <List
          :todos="todos"
          @deleteTodo="deleteTodo"
          @doneTodo="doneTodo"
        />
        <!-- End List Todolist -->

      </div>
    </div>
  </div>

</template>

<script>
import List from './components/List.vue';
export default {
  name: 'App',
  components: {
    List
  },
  data() {
    return {
      todo: "",
      todos: []
    }
  },
  mounted() {
    this.todos = JSON.parse(localStorage.getItem('todos'))
  },
  methods: {
    add() {
      this.todos.unshift({
        activity: this.todo,
        isDone: false
      })
      this.todo = ''
      this.saveToLocalStorage()
    },
    deleteTodo(todoIndex) {
      this.todos = this.todos.filter((item, index) => {
        if (index != todoIndex) {
          return item
        }
      })
      this.saveToLocalStorage()
    },
    doneTodo(todoIndex) {
      this.todos = this.todos.filter((item, index) => {
        if (index == todoIndex) {
          item.isDone = true
        }
        return item;
      })
      this.saveToLocalStorage()
    },
    saveToLocalStorage() {
      localStorage.setItem('todos', JSON.stringify(this.todos))
    }
  },
  computed: {
    totalTODO() {
      return this.todos.length
    }
  }
}
</script>
