<template>
  <div class="animated fadeIn">
    <b-row>
      <b-col sm="6" lg="6">
        <b-card no-body class="bg-warning">
          <b-card-body class="pb-0">
            <h4 class="mb-0">9.823</h4>
            <p>Users</p>
          </b-card-body>
          <card-line3-chart-example style="height:70px;" height="70"/>
        </b-card>
      </b-col>

      <b-col sm="6" lg="6">
        <b-card no-body class="bg-danger">
          <b-card-body class="pb-0">
            <h4 class="mb-0">9.823</h4>
            <p>Articles</p>
          </b-card-body>
          <card-bar-chart-example style="height:70px;" height="70"/>
        </b-card>
      </b-col>
    </b-row>
  </div>
</template>

<script>
import CardLine3ChartExample from './dashboard/CardLine3ChartExample'
import CardBarChartExample from './dashboard/CardBarChartExample'
import { Callout } from '@coreui/vue'

export default {
  name: 'Dashboard',
  components: {},
  data: function () {
    return {}
  },
  created() {
    this.getUserInfo();
    this.getUserInfo();
  },
  computed: {},

  methods: {
    // fetch api data
    getUserInfo() {
      this.axios.get('https://jsonplaceholder.typicode.com/users')
        .then((res) => {
          this.items = res.data;
          console.log(this.items);
        })
        .catch(error => {
          console.log(error.response)
        });
    },
  }
}
</script>

<style>
  /* IE fix */
  #card-chart-01, #card-chart-02 {
    width: 100% !important;
  }
</style>
