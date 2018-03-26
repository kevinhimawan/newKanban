<template>
  <div id="createkanban" class="modal" tabindex="-1" role="dialog">
    <div class="modal-dialog" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title">Add Task</h5>
          <button type="button" class="close" data-dismiss="modal" aria-label="Close">
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div class="modal-body">
          <div class="form-group">
            <label for="name">Please choose a new name</label>
            <input v-model="form.task" type="text" id="task" placeholder="Enter your new task" class="form-control">
          </div>
          <div class="form-group">
            <a class="open-close-description" v-on:click="opendescrption">Description</a>
            <div v-bind:class="{ inactive: description_style }" class="form-group" style="margin-top: 10px;">
              <textarea v-model="form.description" type="text" rows="5" class="form-control" id="description" placeholder="This is optional"></textarea>
            </div>
          </div>
          <div class="form-group">
            <label for="name">Assigned To</label>
            <input v-model="form.member" type="text" id="task" placeholder="Enter your crew" class="form-control">
          </div>
        </div>
        <div class="modal-footer">
          <button type="button" v-on:click="submittask" class="btn btn-primary">Save changes</button>
          <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import swal from 'sweetalert'
export default {
  data () {
    return {
      form:{
        task: '',
        description: '',
        member: ''
      },
      description_style: true,
    }
  },
  methods: {
    submittask () { 
      if (this.form.task === '') {
        swal({
          title: 'Empty Task',
          icon: 'warning',
          button: 'Revise'
        })
      } else {
        $('#createkanban').modal('hide')
        this.$emit('submittask', this.form)
      }
    },
    opendescrption () {
      if (this.description_style === false) {
        this.description_style = true
      } else {
        this.description_style = false
      }
    }
  }
}
</script>

<style scoped>
.form-group{
  text-align: left;
}
.modal-body{
  text-align: left;
}
label{
  font-size: .9em;
}
.description-open:hover{
  text-decoration: none;
}
.inactive{
  display: none;
}
.open-close-description{
  color: #007bff !important;
}
.open-close-description:hover{
  cursor: pointer;
}
</style>
