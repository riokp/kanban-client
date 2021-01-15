<template>

  <div class="">
    <BoardList
    :backlogTasks="backlogTasks"
    :todoTasks="todoTasks"
    :doingTasks="doingTasks"
    :doneTasks="doneTasks"
    :getAllBacklog="getAllBacklog"
    :getAllTodo="getAllTodo"
    :getAllDoing="getAllDoing"
    :getAllDone="getAllDone"
    :getOneTask="getOneTask"
    :taskDetailData="taskDetailData"></BoardList>

  </div>

</template>

<script>
import BoardList from "./BoardList"


export default {
  name: "Home",
  components: {
    BoardList
  },
  props: [
    'tasks',
    'getAllBacklog',
    'getAllTodo',
    'getAllDoing',
    'getAllDone',
    'backlogTasks',
    'todoTasks',
    'doingTasks',
    'doneTasks',
    'add',
    'addTaskData',
    'getOneTask',
    'taskDetailData'
    ]
}
</script>

<style>

</style>