<script setup lang="ts">
import Item from "./Item/Item.vue";
import {ITodo} from "../../typings";

const props = defineProps<{
  userTodoListRef:ITodo[],
  changeTodoState:(uid:string)=> void,
  removeTodoById: (uid:string)=>void
}>()

</script>
<template>
  <Item v-for="item in props.userTodoListRef"
        :id = "item.id"
        :content = "item.content"
        :state = "item.state"
        :key = "item.id"
        :changeTodoState="props.changeTodoState"
        :removeTodoById="props.removeTodoById"
  ></Item>
</template>

<style scoped>

</style>