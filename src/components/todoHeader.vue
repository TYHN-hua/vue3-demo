<script setup>
import {ref, useAttrs} from 'vue'

const attrs = useAttrs()
console.log(attrs)

const props = defineProps({
  modelValue: String
})

console.log(props.modelValue)

const todoName = ref('')
const emit = defineEmits(['addTodo'])
const add = (e) => {
  if (todoName.value) {
    emit('addTodo', todoName.value)
    todoName.value = ''
  }
}
</script>

<template>
  <header class="header">
    <h1>todos</h1>
    <input
      v-model="todoName"
      @keydown.enter="add"
      class="new-todo"
      placeholder="What needs to be done?"
      autofocus
    />
  </header>
</template>

<style lang="less" scoped></style>
