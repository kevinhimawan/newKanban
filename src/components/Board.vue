<template>
  <div>
    <Create
      v-on:submittask="kanbancreate">
    </Create>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <a class="navbar-brand">Kanban Ala Ala</a>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav">
          <li class="nav-item active">
            <a data-toggle="modal" data-target="#createkanban" class="nav-link">Create</a>
          </li>
        </ul>
      </div>
    </nav>
    <Content
    v-bind:taskzero="task0"
    v-bind:taskone="task1"
    v-bind:tasktwo="task2"
    v-bind:taskthree="task3"

    v-on:deletetask="deletetask"
    v-on:nexttask="nexttask"
    v-on:prevtask="prevtask"
    v-on:changekanbandata="changekanban"></Content>
  </div>
</template>

<script>
import Content from '@/components/Content'
import Create from '@/components/Create'
import firebase from 'firebase'
const config = {
  databaseURL: 'https://canban-6918d.firebaseapp.com',
  apiKey: "AIzaSyBV0BNtIxHMbJHGWAwbZNYxWTE-_ZAEojQ",
  authDomain: "canban-6918d.firebaseapp.com",
  projectId: "canban-6918d",
  storageBucket: "canban-6918d.appspot.com",
  messagingSenderId: "284786878901"
}
const firebaseApp = firebase.initializeApp(config)
const db = firebaseApp.database()
const tasksRef = db.ref('task')
export default {
  components: {
    Create, Content
  },
  name: 'Board',
  firebase: {
    tasks: tasksRef
  },
  data () {
    return {
      
    }
  },
  methods: {
    getData () {
      tasksRef.set()
    },
    kanbancreate (value) {
      tasksRef.push({
        task: value.task,
        description: value.description,
        place: 0,
        member: value.member
      })
    },
    deletetask (value) {
      tasksRef.child(value.fireid).set(null)
    },
    nexttask (value) {
      const newStatus = value.status + 1
      tasksRef.child(value.fireid).child('place').set(newStatus)
    },
    prevtask (value) {
      const newStatus = value.status - 1
      tasksRef.child(value.fireid).child('place').set(newStatus)
    },
    changekanban (value) {
      const key = value.value['.key']
      tasksRef.child(key).set({
        description: value.value.description,
        member: value.value.member,
        place: value.value.place,
        task :  value.value.task,
      })
    }
  },
  computed: {
    task0 () {
      return this.tasks.filter(task => task.place === 0)
    },
    task1 () {
      return this.tasks.filter(task => task.place === 1)
    },
    task2 () {
      return this.tasks.filter(task => task.place === 2)
    },
    task3 () {
      return this.tasks.filter(task => task.place === 3)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.navbar {
  padding: 15px 40px !important;
}
.navbar-brand {
  font-family: 'Pacifico', cursive !important;
  font-size: 2em;
  font-weight: 400;
}
.navbar-collapse{
  justify-content: flex-end !important;
}

.nav-link:hover{
  cursor: pointer;
}

.row{
  width: 100%;
  margin: 0;
}
</style>
