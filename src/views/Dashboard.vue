<template>
  <div class="animated fadeIn">
    <b-row>
      <b-col sm="6" lg="6">
        <b-card no-body class="bg-warning">
          <b-card-body class="pb-0">
            <h4 class="mb-0">{{totalUsers}}</h4>
            <p>Users</p>
          </b-card-body>
          <div style="height:70px;" height="70"/>
        </b-card>
      </b-col>

      <b-col sm="6" lg="6">
        <b-card no-body class="bg-danger">
          <b-card-body class="pb-0">
            <h4 class="mb-0">{{totalArticles}}</h4>
            <p>Articles</p>
          </b-card-body>
          <div style="height:70px;" height="70"/>
        </b-card>
      </b-col>
    </b-row>
  </div>
</template>

<script>
export default {
  name: 'Dashboard',
  components: {},
  data: function () {
    return {
      totalUsers: '',
      totalArticles:''
    }
  },
  created() {
    this.getUsers();
    this.getArticles();
  },
  computed: {},

  methods: {
    // fetch user data
    getUsers() {
      this.axios.get('https://jsonplaceholder.typicode.com/users')
        .then((res) => {
          this.totalUsers = res.data.length;
          this.users = res.data;
        })
        .catch(error => {
          console.log(error.response)
        });
    },
    // fetch article data
    getArticles() {
      this.axios.get('https://jsonplaceholder.typicode.com/posts')
        .then((res) => {
          this.totalArticles = res.data.length;
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
