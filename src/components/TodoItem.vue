<template>
  <li>
    <span v-bind:class="{ done: todo.completed, content: true }">
      <input
        type="checkbox"
        v-on:change="todo.completed = !todo.completed"
        v-bind:checked="todo.completed"
      />
      <strong class="index">
        {{ index + 1 }}
      </strong>
      {{ todo.title | uppercase }}
    </span>
    <button class="btn" v-on:click="$emit('remove-todo', todo.id)">
      <img src="../assets/delete.svg" alt="Удалить" />
    </button>
  </li>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      require: true,
    },
    index: Number,
  },
  filters: {
    uppercase(value) {
      console.log(value);
      return value.toUpperCase();
    },
  },
};
</script>

<style scoped>
li {
  display: grid;
  grid-template-columns: 1fr auto;
  margin-bottom: 10px;
  padding: 10px 20px;

  border: 1px solid #ccc;
}

.content {
  display: grid;
  grid-template-columns: 40px 30px auto;
}

.index {
  padding-right: 10px;
}

.btn {
  border-width: 0;
  background-color: inherit;
  cursor: pointer;
}

.btn img {
  width: 12px;
  height: 12px;
}

input {
  cursor: pointer;
}

.done {
  text-decoration: line-through;
  color: #cccccc;
}
</style>
