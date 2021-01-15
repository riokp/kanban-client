<template>

  <div class="board container" id="">
    <div class="board-body">
      <div class="category-title red">
        <h2>Back-log</h2>
      </div>
        <div v-for="(item,index) in backlogTasks" :key="index">
        <TaskItem
        :item="item"
        :backlogTasks="backlogTasks"
        :getOneTask="getOneTask"></TaskItem>
        </div>
    </div>
  </div>

</template>

<script>
import TaskItem from "./TaskItem"

export default {
  name: "TaskBoardBacklog",
  props: [
    "getAllBacklog",
    "backlogTasks",
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