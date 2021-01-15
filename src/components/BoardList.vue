<template>
  
<div class="container">

    <TaskBoardBacklog
    :backlogTasks="backlogTasks"
    :getAllBacklog="getAllBacklog"
    :taskDetailData="taskDetailData"
    :getOneTask="getOneTask"></TaskBoardBacklog>

    <TaskBoardTodo
    :todoTasks="todoTasks"
    :getAllTodo="getAllTodo"
    :taskDetailData="taskDetailData"
    :getOneTask="getOneTask"></TaskBoardTodo>

    <TaskBoardDoing
    :doingTasks="doingTasks"
    :getAllDoing="getAllDoing"
    :taskDetailData="taskDetailData"
    :getOneTask="getOneTask"></TaskBoardDoing>

    <TaskBoardDone
    :doneTasks="doneTasks"
    :getAllDoing="getAllDoing"
    :taskDetailData="taskDetailData"
    :getOneTask="getOneTask"></TaskBoardDone>

</div>


</template>

<script>
import TaskBoardBacklog from "./TaskBoardBacklog"
import TaskBoardTodo from "./TaskBoardTodo"
import TaskBoardDoing from "./TaskBoardDoing"
import TaskBoardDone from "./TaskBoardDone"

export default {
  name: "BoardList",
  props: [
    "tasks",
    'getAllBacklog',
    'getAllTodo',
    'getAllDoing',
    'getAllDone',
    'backlogTasks',
    'todoTasks',
    'doingTasks',
    'doneTasks',
    'taskDetailData',
    'getOneTask'
    ],
  components: {
    TaskBoardBacklog,
    TaskBoardTodo,
    TaskBoardDoing,
    TaskBoardDone
  }
}
</script>

<style>

</style>