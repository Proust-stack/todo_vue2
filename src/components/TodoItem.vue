<template>
  <li>
    <span v-bind:class="{ done: todo.completed }">
      <input type="checkbox" :value="todo.completed" @change="onChange" />
      <strong>{{ index + 1 }}</strong>
      {{ todo.title | upperCase }}
    </span>
    <button class="rm" @click="$emit('removeTodo', todo.id)">&times;</button>
  </li>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true,
    },
    index: Number,
  },
  methods: {
    onChange() {
      // eslint-disable-next-line vue/no-mutating-props
      this.todo.completed = !this.todo.completed;
    },
  },
  filters: {
    upperCase(value) {
      return value.toUpperCase();
    },
  },
};
</script>

<style scoped>
li {
  border: 1px solid #ccc;
  display: flex;
  justify-content: space-between;
  padding: 1rem 0.2rem;
  margin: 1rem;
}
.rm {
  background: blue;
  color: #fff;
  border-radius: 50%;
  font-weight: bold;
  cursor: pointer;
}
.done {
  text-decoration: line-through;
}
input {
  margin-right: 1rem;
}
</style>