<script setup lang="ts">

import {ref} from "vue";
import type {Ref} from "vue";
import {ITodo} from "../../typings";
import {nanoid} from "nanoid"

const props = defineProps<{
  addTodoTings:(userTodoObject:ITodo) => void
}>()

const userInputRef:Ref<string> = ref("")
const addTodo = ():void => {
  if(userInputRef.value.trim().length>0){
    const  userTodoObject:ITodo = {
      id: nanoid(),
      content:userInputRef.value.trim(),
      state:false
    }
    props.addTodoTings(userTodoObject)
    userInputRef.value=""
    return
  }
  alert("Please enter the item after clicking")
}
</script>
<template>
  <input type="text" placeholder="Please add todo things..." v-model="userInputRef"/>
  <button @click="addTodo">Add</button>
</template>

<style scoped>

</style>