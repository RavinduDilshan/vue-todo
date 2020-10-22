<template>
  <div>
    <div v-bind:key="todo.id" v-for="todo in todos">
      <todo_item v-bind:todo="todo" v-on:del-todo="$emit('del-todo',todo.id)"/>
    </div>
  </div>
</template>

<script>

import todo_item from './todo_item';

export default {
  name: "Todos",
  components:{
      todo_item
  },
  props: ["todos"]
};
</script>

<style scoped></style>
