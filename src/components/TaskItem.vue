<template>

  <div class="card col-sm" style="width: 18rem;" id="backlog-task">
    <div class="card-body">
      <h5 class="card-title"><strong>{{item.title}}</strong></h5><hr>
      <p class="card-text">{{item.detail}}</p>
      <p class="card-text">Assigned to: {{item.assign}}</p>
      <button class="btn btn-primary" @click="getOneTask(item.id)">Task detail</button>
    </div>
  </div>

</template>

<script>
export default {
  name: 'TaskItem',
  props: [
    'item',
    'taskDetailData',
    'getOneTask'
    ]
}
</script>

<style>

</style>

