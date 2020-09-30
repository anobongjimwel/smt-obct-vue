<template>
  <div id="buttons">
    <div class="container pt-5">
      <div class="card">
        <div class="card-header">
          <h6>
            <span v-if="state == 'stop'">Inactive</span>
            <span v-if="state == 'start'">Active</span>
          </h6>
        </div>
        <div class="card-body">
          <div class="row">
              <div class="col-12 pb-3">
                  <input v-model="timestamp" class="form-control" placeholder="Email Address"/>
              </div>
          </div> 
          <div class="row">
            <div class="col-md-6">
              <button
                class="btn btn-dark btn-block"
                v-if="state == 'stop'"
                v-on:click="toggleState"
              >
                Start
              </button>
              <button
                class="btn btn-dark btn-block disabled"
                disabled="disabled"
                v-if="state == 'start'"
              >
                Start
              </button>
            </div>
            <div class="col-md-6">
              <button
                class="btn btn-dark btn-block disabled"
                disabled="disabled"
                v-if="state == 'stop'"
              >
                Stop
              </button>
              <button
                class="btn btn-dark btn-block"
                v-if="state == 'start'"
                v-on:click="toggleState"
              >
                Stop
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["state"],
  methods: {
    toggleState: function() {
        this.$parent.toggleState()
    }
  },
  data() {
    return {
        timestamp: ""
    }
  }
};
</script>

<style scoped></style>
