<template>
   <div class="mt-3">
          <ul class="list-group">
            <li class="list-group-item mt-2 " v-for="(todo,index) in todos" :key="index">
            <div class="row">
              <div class="col">
                <span v-if="todo.isDone">
                 <del>{{ todo.activity }}</del>
                </span>
                <span v-else>{{ todo.activity }}</span>
              </div>
              <div class="col-auto">
                  <div class="row gx-2">
                    <div class="col">
                      <button @click="doneTodo(index)" class="btn btn-outline-info">Done</button>
                    </div>
                    <div class="col">
                      <button @click="deleteTodo(index)" class="btn btn-outline-danger">Delete</button>
                    </div>
                  </div>
              </div>
            </div>
            </li>
          </ul>
        </div>
</template>
<script>
export default {
  props: {
    todos: {
      type: Array,
      default: []
    }
  },
  methods: {
    deleteTodo(index) {
      this.$emit('deleteTodo', index)
    },
    doneTodo(index) {
      this.$emit('doneTodo', index)
    }
  }
}
</script>
