<script setup lang="ts">
import Header from "./components/Header/Header.vue";
import List from "./components/List/List.vue";
import Footer from "./components/Footer/Footer.vue";
import {onMounted, ref, watch} from "vue";
import type {Ref} from "vue";
import {ITodo} from "./typings";


const userTodoListRef:Ref<ITodo[]> = ref([])
const addTodoTings = (userTodoObject:ITodo):void => {
  userTodoListRef.value.push(userTodoObject)
}

const changeTodoState = (uid:string):void =>{
  userTodoListRef.value.forEach((todo:ITodo)=>{
    if(todo.id === uid){
      todo.state = !todo.state
    }
  })
}
const removeTodoById = (uid:string):void =>{
  userTodoListRef.value = userTodoListRef.value.filter((todo:ITodo)=>{
    return todo.id !== uid
  })
}
onMounted(()=>{
  const objectSet:ITodo[] = JSON.parse(localStorage.getItem("todoList")||"[]")
  userTodoListRef.value = objectSet
})
watch<Ref<ITodo[]>>(userTodoListRef,()=>{
  localStorage.setItem("todoLIst",JSON.stringify(userTodoListRef.value))
},{
  deep:true
})

</script>

<template>
  <div>
    <Header :addTodoTings="addTodoTings"></Header>
    <List :userTodoListRef="userTodoListRef" :changeTodoState="changeTodoState" :removeTodoById="removeTodoById"></List>
    <Footer :userTodoListRef="userTodoListRef"></Footer>
  </div>
</template>

<style scoped>

</style>
