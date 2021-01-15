<template>

  <div class="board container" id="">
    <div class="board-body">
      <div class="category-title blue">
        <h2>Doing</h2>
      </div>
        <div v-for="(item,index) in doingTasks" :key="index">
        <TaskItem
        :item="item"
        :doingTasks="doingTasks"
        :getOneTask="getOneTask"></TaskItem>
        </div>
    </div>
  </div>

</template>

<script>
import TaskItem from "./TaskItem"

export default {
  name: "TaskBoardDoing",
  props: [
    "doingTasks",
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