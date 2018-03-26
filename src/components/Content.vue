<template>
  <div class="content row col-lg-12">
    <Edit
      v-bind:datakanban="data"
      v-on:changekanban="changekanbandata"></Edit>
    <div class="col-lg-3">
      <div class="title-top" style="background-color:#30bfbf;">
        <h2 class="title-top-font">Ideas</h2>
      </div>
      <div class="card-content">
        <div v-for="(t, index) in taskzero" :key="index" class="card">
          <div class="card-body">
            <div class="task-name">
              <h4 class="task-name-font">{{t.task}}</h4>
            </div>
            <div class="action">
              <a v-on:click="removetask(t)" class="todo-delete-icon" style="padding: 0;border: 0;"><i class="fas fa-trash"></i></a>
              <a data-toggle="modal" data-target="#editKanban" v-on:click="edittask(t)" class="todo-delete-icon" style="padding: 0;border: 0;"><i class="fas fa-edit"></i></a>
              <a v-on:click="next(t)" class="todo-delete-icon" style="padding: 0;border: 0;"><i class="fas fa-arrow-right"></i></a>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="col-lg-3">
      <div class="title-top" style="background-color:#00aaff;">
        <h2 class="title-top-font">Concept</h2>
      </div>
      <div class="card-content">
        <div v-for="(t, index) in taskone" :key="index" class="card">
          <div class="card-body">
            <div class="task-name">
              <h4 class="task-name-font">{{t.task}}</h4>
            </div>
            <div class="action">
              <a v-on:click="prev(t)" class="todo-delete-icon" style="padding: 0;border: 0;"><i class="fas fa-arrow-left"></i></a>
              <a v-on:click="removetask(t)" class="todo-delete-icon" style="padding: 0;border: 0;"><i class="fas fa-trash"></i></a>
              <a data-toggle="modal" data-target="#editKanban" v-on:click="edittask(t)" class="todo-delete-icon" style="padding: 0;border: 0;"><i class="fas fa-edit"></i></a>
              <a v-on:click="next(t)" class="todo-delete-icon" style="padding: 0;border: 0;"><i class="fas fa-arrow-right"></i></a>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="col-lg-3">
      <div class="title-top" style="background-color:#8f7ee6;">
        <h2 class="title-top-font">Prototye</h2>
      </div>
      <div v-for="(t, index) in tasktwo" :key="index" class="card">
        <div class="card-body">
          <div class="task-name">
            <h4 class="task-name-font">{{t.task}}</h4>
          </div>
          <div class="action">
            <a v-on:click="prev(t)" class="todo-delete-icon" style="padding: 0;border: 0;"><i class="fas fa-arrow-left"></i></a>
            <a v-on:click="removetask(t)" class="todo-delete-icon" style="padding: 0;border: 0;"><i class="fas fa-trash"></i></a>
            <a data-toggle="modal" data-target="#editKanban" v-on:click="edittask(t)" class="todo-delete-icon" style="padding: 0;border: 0;"><i class="fas fa-edit"></i></a>
            <a v-on:click="next(t)" class="todo-delete-icon" style="padding: 0;border: 0;"><i class="fas fa-arrow-right"></i></a>
          </div>
        </div>
      </div>
    </div>
    <div class="col-lg-3">
      <div class="title-top" style="background-color:#e85a5a;">
        <h2 class="title-top-font">Done</h2>
      </div>
      <div v-for="(t, index) in taskthree" :key="index" class="card">
        <div class="card-body">
          <div class="task-name">
            <h4 class="task-name-font">{{t.task}}</h4>
          </div>
          <div class="action">
            <a v-on:click="prev(t)" class="todo-delete-icon" style="padding: 0;border: 0;"><i class="fas fa-arrow-left"></i></a>
            <a v-on:click="removetask(t)" class="todo-delete-icon" style="padding: 0;border: 0;"><i class="fas fa-trash"></i></a>
            <a data-toggle="modal" data-target="#editKanban" v-on:click="edittask(t)" class="todo-delete-icon" style="padding: 0;border: 0;"><i class="fas fa-edit"></i></a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import Edit from '@/components/Edit'
export default {
  components: {
    Edit
  },
  data () {
    return {
      data: {}
    }
  },
  props: ['taskzero', 'taskone', 'tasktwo', 'taskthree'],
  methods: {
    removetask (keyfire) {
      this.$emit('deletetask', {fireid: keyfire['.key']})
    },
    next(keyfire) {
      this.$emit('nexttask', {fireid: keyfire['.key'], status: keyfire['place']})
    },
    edittask (keyfire) {
      this.data = keyfire
    },
    prev (keyfire) {
      this.$emit('prevtask', {fireid: keyfire['.key'], status: keyfire['place']})
    },
    changekanbandata (value) {
      this.$emit('changekanbandata', {value:value})
    }
  }
}
</script>

<style scoped>
.row{
  padding: 40px 0 !important;
  width: 100%;
}
.title-top{
  padding: 10px 20px;
  margin-bottom: 20px;
}
.title-top-font{
  font-size: 1.4em;
  text-align: left;
  margin: 0;
  color: white;
}
.card{
  margin-bottom: 15px;
  box-shadow: 0px 1px 1px 0px rgba(130,145,153,0.5);
  border: none !important
}
.card-body{
  display: flex;
  padding: 10px 15px;
  flex-direction: column;
}
.task-name{
  text-align: left;
  padding: 0;
  margin-bottom: 10px;
}
.task-name-font{
  margin:0;
  font-size: 1.1em;
}
.action{
  padding: 0;
  display: flex;
  justify-content: flex-start;
  align-items: center;
}
.col-lg-3{
  padding: 0
}
.card-content{
  padding: 0 15px;
}
.todo-delete-icon{
  font-size: .8em;
  margin: 0 5px;
}
.todo-delete-icon:hover{
  cursor: pointer;
}
</style>
