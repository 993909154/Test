<template>
  <div>
    <div>
      <input type="text" v-model="title" />
      <button @click="addTodo">+</button>
    </div>
    <todo-item v-for="item in filtersTodos" :key="item.id" :todo="item" />
    <button @click="show('all')">All</button>
    <button @click="show('active')">Active</button>
    <button @click="show('completed')">Completed</button>
    <button @click="clean">Clean</button>
  </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";
export default {
  name: "TodoApp",
  props: {},
  components: {
    TodoItem
  },
  computed: {
    filtersTodos: function() {
      const filters = {
        all: function(todos) {
          return todos;
        },
        active: function(todos) {
          return todos.filter(t => !t.completed);
        },
        completed: function(todos) {
          return todos.filter(t => t.completed);
        }
      };
      return filters[this.visibility](this.todos);
    }
  },
  data() {
    return {
      title: "",
      todos: [],
      id: 0,
      visibility: "all"
    };
  },
  methods: {
    addTodo() {
      const newTodo = {
        id: this.id++,
        title: this.title,
        completed: false
      };
      this.todos.push(newTodo);
      this.title = "";
    },
    show(visibility) {
      this.visibility = visibility;
    },
    clean() {
      this.todos = this.todos.filter(t => !t.completed)
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
