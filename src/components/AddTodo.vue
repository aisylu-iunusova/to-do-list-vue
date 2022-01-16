<template>
  <form @submit.prevent="onSubmit">
    <input type="text" v-model="title" />
    <button type="submit">Добавить</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      title: "",
    };
  },
  methods: {
    onSubmit() {
      console.log("Submit", this.title);
      if (this.title.trim()) {
        console.log("test 1");
        const newTodo = {
          id: Date.now(),
          title: this.title,
          complete: false,
        };

        this.$emit("add-todo", newTodo);
        this.title = "";
      }
    },
  },
};
</script>

<style scoped>
form {
  display: flex;
  padding-right: 20px;
}

input {
  width: 400px;
  border-width: 0;
  border-bottom: 1px solid #000;
  margin-right: 20px;
  padding: 10px 20px;
}

button {
  cursor: pointer;
  font-weight: 14px;
  background-color: #fff;
  border-radius: 5px;
  border: 1px solid #2c3e50;
  padding: 0 10px;
}
</style>
