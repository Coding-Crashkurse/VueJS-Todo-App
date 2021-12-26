<template>
  <div
    class="flex justify-between items-center py-4 px-2 border-t-2 border-black"
    :class="{ 'bg-green-600': this.todo.done, 'bg-red-500': !this.todo.done }"
  >
    <p class="cursor-pointer" @click="toggleTodo">
      {{ todo.todo }}
    </p>
    <button class="py-2 px-4 bg-black rounded" @click="removeTodo">
      Delete Todo
    </button>
  </div>
</template>

<script>
export default {
  name: "Todo",
  props: ["todoprop", "todoindex"],
  data() {
    return {
      todo: this.todoprop,
    };
  },
  methods: {
    toggleTodo() {
      this.$emit("toggledone-index", this.todoindex);
    },
    removeTodo() {
      this.$emit("remove-index", this.todoindex);
    },
  },
};
</script>
