<template>
  <div class="text-white bg-gray-600 w-2/4 max-w-2xl m-auto mt-12">
    <div class="text-center border-b-2 border-black py-4">
      <h1 class="text-3xl py-4">Unsere Todos</h1>

      <p class="text-xl p-2" v-if="openTodos.length > 0">
        Offene Todos: {{ openTodos.length }}
      </p>
      <p class="text-xl p-2" v-else>Gratuliere: Keine Todos!</p>
      <div class="flex space-around">
        <input
          type="text"
          v-model="newTodo"
          class="py-2 px-2 text-black inline-block w-2/3"
        />
        <button
          class="w-1/3 border-black border-2 bg-yellow-500"
          @click="addTodo"
        >
          Add Todo
        </button>
      </div>
    </div>
    <div v-for="(todo, index) in todos" :key="todo.todo">
      <Todo :todoprop="todo" :todoindex="index" @child-index="removeTodo" />
    </div>
  </div>
</template>

<script>
import Todo from "./components/Todo.vue";

export default {
  name: "App",
  components: {
    Todo,
  },
  data() {
    return {
      newTodo: "",
      todos: [
        { todo: "Einkaufen", done: false },
        { todo: "Sport", done: false },
        { todo: "Programmieren", done: true },
      ],
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() === "") {
        return;
      }
      this.todos.push({ todo: this.newTodo, done: false });
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
  },
  computed: {
    openTodos() {
      const openTodos = this.todos.filter((todo) => {
        return !todo.done;
      });
      return openTodos;
    },
  },
};
</script>
