<template>
  
  <div class="container card-body" id="add-form">
    <form @submit.prevent="add">
      <div class="mb-4">
        <label for="add-form-title" class="form-label">Title</label>
        <input v-model="addTaskData.title" type="text" class="form-control" id="add-form-title" placeholder="Task title">
      </div>
      <div class="mb-4">
        <label for="add-form-detail" class="form-label">Detail</label>
        <input v-model="addTaskData.detail" type="text" class="form-control" id="add-form-detail" placeholder="Task detail">
      </div>
      <div class="mb-4">
        <label for="add-form-assign" class="form-label">Assigned to</label>
        <input v-model="addTaskData.assign" type="text" class="form-control" id="add-form-assign" placeholder="Assign someone to this task">
      </div>
      <small id="emailHelp" class="form-text text-muted">all newly created tasks will be automatically logged as a backlog</small><br><br>
      <button type="submit" class="btn btn-primary">Add</button>
      <button @click.prevent="switchPage('home')" class="btn btn-info ">Cancel</button>
    </form>
  </div>

</template>

<script>
export default {
  name: "AddForm",
  props: ["addTaskData","add","switchPage"]
}
</script>

<style>

</style>