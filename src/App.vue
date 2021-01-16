<template>

   <div class="">

<!-- NAVBAR -->
     <Navbar
     :switchPage="switchPage"
     :currentPage="currentPage"
     :logout="logout"></Navbar>

<!-- REGISTER PAGE -->
     <div v-if="currentPage == 'register'">

     <RegisterForm
     :register="register"
     :registerData="registerData"
     :switchPage="switchPage"
     :currentPage="currentPage"
     :onSignIn="onSignIn"></RegisterForm>
     </div>

<!-- LOGIN PAGE -->
     <div v-else-if="currentPage == 'login'">

     <LoginForm
     v-if="currentPage == 'login'"
     :login="login"
     :loginData="loginData"
     :switchPage="switchPage"
     :currentPage="currentPage"
     :onSignIn="onSignIn"></LoginForm>
     </div>

<!-- HOME PAGE -->
     <div v-else-if="currentPage == 'home'">

     <Home
     :backlogTasks="backlogTasks"
     :todoTasks="todoTasks"
     :doingTasks="doingTasks"
     :doneTasks="doneTasks"
     :getAllBacklog="getAllBacklog"
     :getAllTodo="getAllTodo"
     :getAllDoing="getAllDoing"
     :getAllDone="getAllDone"
     :add="add"
     :addTaskData="addTaskData"
     :getOneTask="getOneTask"
     :taskDetailData="taskDetailData"></Home>
     </div>

<!-- HOME PAGE -->
     <div v-else-if="currentPage == 'add'">
      <AddForm
      :add="add"
      :addTaskData="addTaskData"
      :switchPage="switchPage"></AddForm>

      <Home
      :backlogTasks="backlogTasks"
      :todoTasks="todoTasks"
      :doingTasks="doingTasks"
      :doneTasks="doneTasks"
      :getAllBacklog="getAllBacklog"
      :getAllTodo="getAllTodo"
      :getAllDoing="getAllDoing"
      :getAllDone="getAllDone"
      :add="add"
      :addTaskData="addTaskData"
      :getOneTask="getOneTask"
      :taskDetailData="taskDetailData"></Home>
     </div>

<!-- DETAIL PAGE -->
    <div v-else-if="currentPage == 'detail'">
      <TaskDetail
      :update="update"
      :taskDetailData="taskDetailData"
      :switchPage="switchPage"
      :deleteTask="deleteTask"></TaskDetail>
    </div>
   </div>
   
</template>

<script>
import axios from "axios"
import RegisterForm from "./components/RegisterForm"
import LoginForm from "./components/LoginForm"
import Home from "./components/Home"
import Navbar from "./components/Navbar"
import TaskDetail from "./components/TaskDetail"
import AddForm from "./components/AddForm"
import GoogleSignInButton from 'vue-google-signin-button-directive'

export default {
  name: 'App',
  directives: {
    GoogleSignInButton
  },
  data() {
    return {
      clientId: '896738878495-o85tsaaedg4jgvunib0mun4cdk1c6600.apps.googleusercontent.com',
      currentPage: "register",
      baseUrl: "https://stormy-tor-29734.herokuapp.com",
      tasks: [],
      backlogTasks: [],
      todoTasks: [],
      doingTasks: [],
      doneTasks: [],
      registerData: {
        name: "",
        email: "",
        password: ""
      },
      loginData: {
        email: '',
        password: ''
      },
      addTaskData: {
        title: '',
        detail: '',
        assign: ''
      },
      taskDetailData : {
        title: '',
        detail: '',
        assign: '',
        category: ''
      },
      categoryName: ""
    }
  },
  components: {
    Navbar,
    Home,
    RegisterForm,
    LoginForm,
    TaskDetail,
    AddForm
  },
  methods: {
    checkAuth() {
      if(localStorage.getItem('access_token')) {
        this.switchPage('home');
        this.getAllBacklog();
        this.getAllTodo();
        this.getAllDoing();
        this.getAllDone();
      } else {
        this.switchPage('register')
      }
    },
    switchPage(page) {
      this.currentPage = page
    },
    register() {
      axios({
        method: 'POST',
        url: this.baseUrl+'/register',
        data: this.registerData
      }).then(response => {
        console.log(response);
        this.switchPage('login')
        this.registerData = ""
      }).catch(err => {
        console.log(err);
      })
    },
    login() {
      axios({
        method: 'POST',
        url: `${this.baseUrl}/login`,
        data: this.loginData
      }).then(response => {
        console.log(response)
        localStorage.setItem("access_token",response.data.access_token)
        this.checkAuth()
        this.switchPage('home')
      }).catch(err => {
        console.log(err);
      })
    },
    logout() {
      localStorage.clear()
      this.switchPage('register')
      const auth2 = gapi.auth2.getAuthInstance();
      auth2.signOut().then(function () {
        console.log('User signed out.');
      });
    },
    getAllTask() {
      axios({
        method: 'GET',
        url: "https://stormy-tor-29734.herokuapp.com/tasks",
        headers: {
          access_token: localStorage.getItem('access_token')
        }
      })
      .then(response => {
        this.tasks = response.data
      })
      .catch(err => {
        console.log(err.response);
      })
    },
    getAllBacklog() {
      axios({
        method: 'GET',
        url: this.baseUrl+'/tasks/backlog',
        headers: {
          access_token: localStorage.getItem('access_token')
        }
      })
      .then(response => {
        this.backlogTasks = response.data
      })
      .catch(err => {
        console.log(err.response);
      })
    },
    getAllTodo() {
      axios({
        method: 'GET',
        url: this.baseUrl+'/tasks/todo',
        headers: {
          access_token: localStorage.getItem('access_token')
        }
      })
      .then(response => {
        this.todoTasks = response.data
      })
      .catch(err => {
        console.log(err.response);
      })
    },
    getAllDoing() {
      axios({
        method: 'GET',
        url: this.baseUrl+'/tasks/doing',
        headers: {
          access_token: localStorage.getItem('access_token')
        }
      })
      .then(response => {
        this.doingTasks = response.data
      })
      .catch(err => {
        console.log(err.response);
      })
    },
    getAllDone() {
      axios({
        method: 'GET',
        url: this.baseUrl+'/tasks/done',
        headers: {
          access_token: localStorage.getItem('access_token')
        }
      })
      .then(response => {
        this.doneTasks = response.data
      })
      .catch(err => {
        console.log(err.response);
      })
    },
    getOneTask(id) {
      axios ({
        method: 'GET',
        url: `https://stormy-tor-29734.herokuapp.com/tasks/${id}`,
        headers: {
          access_token: localStorage.getItem('access_token')
        }
      })
      .then(response => {
        this.taskDetailData = response.data
        console.log(this.taskDetailData);
        this.switchPage('detail')
      })
      .catch(err => {
        console.log(err);
      })
    },
    add() {
      axios({
          method: 'POST',
          url: `${this.baseUrl}/tasks`,
          data: this.addTaskData,
          headers: {
            access_token: localStorage.access_token
          }
        })
      .then(response => {
        console.log(response);
        this.addTaskData = ''
        this.checkAuth()
      })
      .catch(err => {
        console.log(err.response);
      })
    },
    update(id) {
      axios({
        method: 'PUT',
        url: `${this.baseUrl}/tasks/${id}`,
        data: this.taskDetailData,
        headers: {
          access_token: localStorage.access_token
        }
      })
      .then(response => {
        this.checkAuth()
        this.taskDetailData.title = '';
        this.taskDetailData.detail = '';
        this.taskDetailData.assign = '';
      })
      .catch(err => {
        console.log(err);
      })
    },
    patch(id, category) {
      axios({
        method: 'PATCH',
        url: `${this.baseUrl}/tasks/${id}`,
        data: {
          category
        },
        headers: {
          access_token: localStorage.access_token
        }
      })
      .then(response => {
        this.checkAuth();
        console.log(response);
      })
      .err(err => {
        console.log(err);
      })
    },
    deleteTask(id) {
      axios({
        method: 'DELETE',
        url: `${this.baseUrl}/tasks/${id}`,
        headers: {
          access_token: localStorage.access_token
        }
      })
      .then(response => {
        this.checkAuth()
        console.log(response);
      })
      .err(err => {
        console.log(err);
      })
    },
    onSignIn(googleUser) {
      const id_token = googleUser.getAuthResponse().id_token;
      console.log(id_token);
      axios({
        method: 'POST',
        url: `https://stormy-tor-29734.herokuapp.com/googleSignIn`,
        data: {id_token: id_token}
      })
      .done(response => {
        console.log(response);
        localStorage.setItem(`access_token`,response.access_token)
      })
      .fail((xhr,status) => {
      })
    }
  },
  created() {
    this.checkAuth();
  }
}
</script>

<style>

</style>