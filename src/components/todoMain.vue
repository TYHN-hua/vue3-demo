<script setup>
import {computed} from "vue";

const props = defineProps({
  list: {
    type: Array,
    default: () => ([])
  }
})

const emits = defineEmits(['changeFn', 'delTodo', 'checkAll'])

const changeFn = (id) => {
  emits('changeFn', id)
}

const delTodo = (id) => {
  emits('delTodo', id)
}

const isCheckAll = computed({
  get() {
    return props.list.every(item => item.done)
  },
  set(val) {
    emits('checkAll', val)
  }
})

</script>

<template>
  <section class="main">
    <input id="toggle-all" class="toggle-all" type="checkbox" v-model="isCheckAll"/>
    <label for="toggle-all">Mark all as complete</label>
    <ul class="todo-list">
      <li :class="{completed: item.done}" v-for="item in list" :key="item.id">
        <div class="view">
          <input @click="changeFn(item.id)" class="toggle" type="checkbox" :checked="item.done"/>
          <label>{{ item.name }}</label>
          <button @click="delTodo(item.id)" class="destroy"></button>
        </div>
        <input class="edit" value="Create a TodoMVC template"/>
      </li>
      <!--      <li>-->
      <!--        <div class="view">-->
      <!--          <input class="toggle" type="checkbox" />-->
      <!--          <label>Buy a unicorn</label>-->
      <!--          <button class="destroy"></button>-->
      <!--        </div>-->
      <!--        <input class="edit" value="Rule the web" />-->
      <!--      </li>-->
    </ul>
  </section>
</template>

<style lang="less" scoped></style>
