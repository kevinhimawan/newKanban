<template>
  <div id="editKanban" class="modal" tabindex="-1" role="dialog">
    <div class="modal-dialog" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title">Edit Kanban</h5>
          <button type="button" class="close" data-dismiss="modal" aria-label="Close">
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div class="modal-body">
          <div class="form-group">
            <label for="name">Please choose a new name</label>
            <input v-model="datakanban.task" type="text" id="task" placeholder="Enter your new task" class="form-control">
          </div>
          <div class="form-group">
            <div class="form-group" style="margin-top: 10px;">
              <textarea v-model="datakanban.description" type="text" rows="5" class="form-control" id="description" placeholder="This is optional"></textarea>
            </div>
          </div>
          <div class="form-group">
            <label for="name">Assigned To</label>
            <input v-model="datakanban.member" type="text" id="task" placeholder="Enter your crew" class="form-control">
          </div>
        </div>
        <div class="modal-footer">
          <button v-on:click="submitform" type="button" class="btn btn-primary">Save changes</button>
          <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['datakanban'],
  methods: {
    submitform () {
      this.$emit('changekanban', this.datakanban)
      $('#editKanban').modal('hide')
    }
  }
}
</script>

<style>
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
