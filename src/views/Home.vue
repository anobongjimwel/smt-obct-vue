<template>
  <div id="home">
    <div class="home">
      <Buttons :state="state" />
      <Logs :logs="logs" />
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from "@/components/HelloWorld.vue";
import Buttons from "@/components/Buttons.vue";
import Logs from "@/components/Logs.vue";
import Vue from 'vue'
import axios from 'axios';
import VueAxios from 'vue-axios';
Vue.use(VueAxios, axios);

export default {
  components: {
    // HelloWorld
    Buttons,
    Logs
  },
  data() {
    return {
      state: "stop",
      logs: []
    };
  },
  methods: {
    toggleState: function() {
      let self = this;
      console.log(this.timestamp)
      Vue.axios.post('http://localhost:3000/api/log', {log_type: this.state == "stop" ? "start" : "stop", timestamp: this.timestamp})
        .then(result => {
          console.log(result.data.success);
          if (result.data.success == true) {
            self.state = self.state == "stop" ? "start" : "stop"
          }
        })
      this.getAllLogs();
    },
    getAllLogs: function() {
      let self = this;
      Vue.axios.get('http://localhost:3000/api/logs')
        .then(result => self.logs = result.data);
    },
    deleteLog: function(id) {
      let self = this;
      Vue.axios.delete('http://localhost:3000/api/logs/'+id)
        .then(result => {
          if (result.data.success == true) {
            self.getAllLogs();
          }
        });
    }
  },
  created() {
    let self = this;
      Vue.axios.get('http://localhost:3000/api/logs')
        .then(result => self.logs = result.data);
  }
};
</script>

<style>
.card {
  box-shadow: 0 0 10px gainsboro;
}
</style>
