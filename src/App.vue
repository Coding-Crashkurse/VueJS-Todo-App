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
      <Todo
        :todoprop="todo"
        :todoindex="index"
        @remove-index="removeTodo"
        @toggledone-index="setDone"
      />
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
      todos: [],
    };
  },
  mounted() {
    let data = localStorage.getItem("todos");
    console.log(data);
    if (data !== "" && data !== null) {
      this.todos = JSON.parse(data);
    } else {
      this.todos = [];
    }
  },
  methods: {
    storeTodos() {
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
    addTodo() {
      if (this.newTodo.trim() === "") {
        return;
      }
      this.todos.push({ todo: this.newTodo, done: false });
      this.storeTodos();
      this.newTodo = "";
    },
    setDone(index) {
      this.todos[index].done = !this.todos[index].done;
      this.storeTodos();
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
      this.storeTodos();
    },
  },
  computed: {
    openTodos() {
      console.log(this.todos);
      const openTodos = this.todos.filter((todo) => {
        return !todo.done;
      });
      return openTodos;
    },
  },
};
</script>
