<template>
  <div>
    <input type="checkbox" v-model="todo.completed" />
    <u v-if="todo.completed">{{ todo.title }}</u>
    <span v-else>
      <input type="text" v-if="isEdit" v-model="todo.title" @keyup="keyup"/>
      <p v-else  @dblclick="edit">{{ todo.title }}</p>
    </span>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: {
    todo: Object
  },
  data() {
    return {
      isEdit:false
    };
  },
  methods: {
    edit(){
      this.isEdit = true
    },
    keyup(e){
      if(e.keyCode === 13){
        this.isEdit = false
      }
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
