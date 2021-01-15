<template>

  <div class="board container" id="">
    <div class="board-body">
      <div class="category-title green">
        <h2>Done</h2>
      </div>
        <div v-for="(item,index) in doneTasks" :key="index">
        <TaskItem
        :item="item"
        :doneTasks="doneTasks"
        :getOneTask="getOneTask"></TaskItem>
        </div>
    </div>
  </div>

</template>

<script>
import TaskItem from "./TaskItem"

export default {
  name: "TaskBoardDone",
  props: [
    "doneTasks",
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