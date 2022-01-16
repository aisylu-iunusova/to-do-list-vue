<template>
  <div>
    <h2>To-do list</h2>
    <router-link to="/">Back to home page</router-link>
    <div class="content">
      <div class="header">
        <AddTodo v-on:add-todo="addTodo" />
        <select class="filter" v-model="filter">
          <option value="all">All</option>
          <option value="completed">Completed</option>
          <option value="not-completed">Not completed</option>
        </select>
      </div>
      <div>
        <Loader v-if="loading" />
        <TodoList
          v-else-if="filteredTodos.length"
          v-bind:todos="filteredTodos"
          v-on:remove-todo="removeTodo"
        />
        <p v-else>No todos!</p>
      </div>
    </div>
  </div>
</template>

<script>
import TodoList from "../components/TodoList";
import AddTodo from "../components/AddTodo";
import Loader from "../components/Loader";

export default {
  data() {
    return {
      todos: [],
      loading: true,
      filter: "all",
    };
  },
  mounted() {
    fetch("https://jsonplaceholder.typicode.com/todos?_limit=5")
      .then((response) => response.json())
      .then((json) => {
        setTimeout(() => {
          this.todos = json;
          this.loading = false;
        }, 500);
      });
  },
  computed: {
    filteredTodos() {
      if (this.filter === "all") {
        return this.todos;
      }

      if (this.filter === "completed") {
        return this.todos.filter((t) => t.completed);
      }

      if (this.filter === "not-completed") {
        return this.todos.filter((t) => !t.completed);
      }

      return [];
    },
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
    addTodo(todo) {
      this.todos.push(todo);
    },
  },
  components: {
    TodoList,
    AddTodo,
    Loader,
  },
};
</script>

<style>
.header {
  display: flex;
  margin-top: 20px;
}

.filter {
  cursor: pointer;
  border-radius: 5px;
  padding: 0 20px;
  width: 100%;
}

.content {
  display: flex;
  flex-direction: column;
  gap: 20px;
}
</style>
