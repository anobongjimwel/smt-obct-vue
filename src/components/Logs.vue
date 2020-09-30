<template>
  <div class="container pt-4 pb-5">
    <div class="card">
      <div class="card-body">
        <div v-for="log in logs" v-bind:key="log.id" class="row entry">
          <div class="col-md-10">
            <h6 class="text-danger" v-if="log.log_type == 'stop'">Stopped</h6>
            <h6 class="text-success" v-if="log.log_type == 'start'">Started</h6>
            <h5>{{ log.timestamp }}</h5>
          </div>
          <div class="col-md-2">
            <button class="align-self-center btn btn-danger" @click="deleteLog(log._id)">Delete</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
    props: ["logs"],
    methods: {
        deleteLog: function(id) {
            this.$parent.deleteLog(id)
        }
    }
};
</script>

<style scoped>
.entry:not(:last-child) {
  border-bottom: 1px solid gainsboro;
}

.entry {
  padding: 20px 10px;
  margin: 0 10px;
}
</style>
