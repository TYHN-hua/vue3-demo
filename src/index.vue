<script setup>
import './styles/base.css'
import './styles/index.css'
import TodoHeader from './components/TodoHeader.vue'
import TodoMain from './components/TodoMain.vue'
import TodoFooter from './components/TodoFooter.vue'
import {reactive, ref, watch} from "vue";

// 提供数据
/**
 * @type {{name: string, id: number, done: false}[]}
 */
const list = ref(JSON.parse(localStorage.getItem('todo')) || [])
const changeFn = (id) => {
  list.value.forEach(item => {
    if (item.id === id) {
      item.done = !item.done
    }
  })
}

const delTodo = (id) => {
  list.value = list.value.filter(item => item.id !== id)
}

const addTodo = (name) => {
  list.value.push({
    name,
    id: Math.random(),
    done: false
  })
}

watch(list.value, () => {
  localStorage.setItem('todo', JSON.stringify(list.value))
}, {
  deep: true
})

const checkAll = (status) => {
  list.value.forEach(item => item.done = status)
}
</script>

<template>
  <section class="todoapp">
    <TodoHeader v-model="list" @addTodo="addTodo"></TodoHeader>
    <TodoMain @checkAll="checkAll" @delTodo="delTodo" @changeFn="changeFn" :list="list"></TodoMain>
    <TodoFooter :list="list"></TodoFooter>
  </section>
</template>

<style></style>
