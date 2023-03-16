<script setup lang="ts">
import {ITodo} from "../../typings";
import {computed} from "vue";
import type {ComputedRef} from "vue";

const props = defineProps<{
  userTodoListRef:ITodo[]
}>()

const countTodoRef:ComputedRef<number> = computed(()=>{
  return props.userTodoListRef.reduce((pre:number,curr:ITodo)=>{
    return pre += (curr.state === true ? 1 : 0)
  },0)
})
</script>
<template>
  <p>Total:{{countTodoRef}}</p>
</template>

<style scoped>

</style>