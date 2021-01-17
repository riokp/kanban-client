<template>

  <div class="card col-sm container" style="width: 20rem;" id="task-detail">
    <form class="form-group" @submit.prevent="update(taskDetailData.id)" method="post">
      <div class="card-body">
        <h5 class="card-title"><strong>Task details</strong></h5><hr>
        <label for="">Task</label>
        <input class="form-control" v-model="taskDetailData.title" type="text" value="asdas"><br>
        <label for="">Description</label>
        <input class="form-control" v-model="taskDetailData.detail" type="text" value=""><br>
        <label for="">Assign to</label>
        <input class="form-control" v-model="taskDetailData.assign" type="text" value=""><br>
        <label for="">Status</label>
        <select class="form-control" v-model="taskDetailData.category" name="" id="">
          <option value="backlog">Backlog</option>
          <option value="todo">To-do</option>
          <option value="doing">Doing</option>
          <option value="done">Done</option>
        </select><br>
        <br>
        <button class="btn btn-primary" type="submit">Save</button>
        <button class="btn btn-danger" @click="deleteTask(taskDetailData.id)">Delete</button>
        <a href="#" @click.prevent="switchPage('home')" class="btn btn-info">Cancel</a>
      </div>
    </form>
  </div>

</template>

<script>
export default {
  name: "TaskDetail",
  props: ["taskDetailData","update","switchPage",'deleteTask']
}
</script>

<style>

</style>