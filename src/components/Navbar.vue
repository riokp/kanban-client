<template>

    <nav class="navbar navbar-light px-3 header">
      <div class="logo">
        <h3>KanbanApp</h3>
      </div>
      <div class="nav-link">
        <a href="#" v-if="currentPage === 'login'" @click="switchPage('register')">register</a>
        <a href="#" v-if="currentPage === 'register'" @click="switchPage('login')">log in</a>
        <a href="#" v-if="currentPage === 'home' || currentPage == 'add'" @click="switchPage('add')">add task</a>
        <a href="#" v-if="currentPage === 'home' || currentPage == 'add'" @click="logout">logout</a>
      </div>
    </nav>
  
</template>

<script>

export default {
  name: "Navbar",
  props: ['switchPage','currentPage',"logout"]
}
</script>

<style>

</style>