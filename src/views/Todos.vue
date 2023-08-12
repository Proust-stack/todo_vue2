<template>
  <div>
    <h2>Enjoy your work</h2>

    <router-link class="link" to="/">return to home page</router-link>
    <hr />
    <AddTodo @add-todo="addTodo" />
    <select v-model="filter">
      <option value="all">all</option>
      <option value="completed">completed</option>
      <option value="in-progress">in progress</option>
    </select>
    <hr />
    <SimpleLoader v-if="loading" />
    <TodoList
      v-bind:todos="filteredTodos"
      @remove-todo="romoveTodo"
      v-else-if="filteredTodos.length"
    />
    <p v-else>No todos</p>
  </div>
</template>
  
  <script>
import TodoList from "@/components/TodoList.vue";
import AddTodo from "@/components/AddTodo.vue";
import SimpleLoader from "@/components/SimpleLoader.vue";
export default {
  name: "App",
  data() {
    return {
      todos: [],
      loading: true,
      filter: "all",
    };
  },
  components: {
    TodoList,
    AddTodo,
    SimpleLoader,
  },
  mounted() {
    fetch("https://jsonplaceholder.typicode.com/todos?_limit=3")
      .then((response) => response.json())
      .then((json) => {
        this.todos = json;
        this.loading = false;
      });
  },
  // watch: {
  //   filter(value) {
  //     console.log(value)
  //   }
  // },
  computed: {
    // eslint-disable-next-line vue/return-in-computed-property
    filteredTodos() {
      if (this.filter === "all") {
        return this.todos;
      }
      if (this.filter === "completed") {
        return this.todos.filter((todo) => todo.completed);
      }
      if (this.filter === "in-progress") {
        return this.todos.filter((todo) => !todo.completed);
      }
    },
  },
  methods: {
    romoveTodo(id) {
      // eslint-disable-next-line vue/no-mutating-props
      this.todos = this.todos.filter((todo) => todo.id != id);
      console.log("remove-todo in app");
    },
    addTodo(todo) {
      this.todos.push(todo);
    },
  },
};
</script>
  
  <style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  width: 40%;
}
.link {
  text-decoration: none;
  margin-top: 1rem;
}
</style>
  