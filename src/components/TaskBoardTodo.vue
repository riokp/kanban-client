<template>

  <div class="board container" id="">
    <div class="board-body">
      <div class="category-title yellow">
        <h2>To-do</h2>
      </div>
        <div v-for="(item,index) in todoTasks" :key="index">
        <TaskItem
        :item="item"
        :todoTasks="todoTasks"
        :getOneTask="getOneTask"></TaskItem>
        </div>
    </div>
  </div>

</template>

<script>
import TaskItem from "./TaskItem"

export default {
  name: "TaskBoardTodo",
  props: [
    "todoTasks",
    'taskDetailData',
    'getOneTask'
    ],
  components: {
    TaskItem,
  }
}
</script>

<style>

</style>