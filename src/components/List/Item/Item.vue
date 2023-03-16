<script setup lang="ts">

const props = defineProps<{
  id:string,
  content:string,
  state:boolean,
  changeTodoState:(uid:string)=> void,
  removeTodoById:(uid:string)=> void
}>()
const changeState = () => {
  props.changeTodoState(props.id)
}
const removeTodo = () =>{
  props.removeTodoById(props.id)
}
</script>
<template>
  <p>
    <input type="checkbox" :checked="state" @change="changeState">
    <span :class="{completed:state}">{{props.content}}</span>
    <button v-if="state" @click="removeTodo">Remove</button>
  </p>
</template>

<style scoped>
  .completed {
    text-decoration: line-through;
  }
</style>