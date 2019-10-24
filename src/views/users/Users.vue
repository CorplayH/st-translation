<template>

  <b-row>
    <b-col cols="12" xl="12">
      <!--search box-->
      <b-card>
        <h3>Search by name</h3>
        <input type="text" name="name" class="form-control" v-model="search">
        <div v-if="search.length !== 0" class="mt-2">
          {{filteredList.length}} user found
        </div>
      </b-card>
      <!--end search box-->
      <!--User table-->
      <transition name="slide">
        <b-card>
          <div slot="header" v-html="caption"></div>
          <b-table :hover="hover" :striped="striped" :bordered="bordered" :small="small" :fixed="fixed" responsive="sm"
                   :items="filteredList" :fields="fields"
                   :current-page="currentPage" :per-page="perPage" @row-clicked="rowClicked">
          </b-table>
          <nav>
            <b-pagination size="md" :total-rows="getRowCount(users)" :per-page="perPage" v-model="currentPage" prev-text="Prev" next-text="Next" hide-goto-end-buttons/>
          </nav>
        </b-card>
      </transition>
      <!--end user table-->
    </b-col>
  </b-row>
</template>

<script>
  export default {
    name: 'Users',
    props: {
      caption: {
        type: String,
        default: 'Users'
      },
      hover: {
        type: Boolean,
        default: true
      },
      striped: {
        type: Boolean,
        default: true
      },
      bordered: {
        type: Boolean,
        default: false
      },
      small: {
        type: Boolean,
        default: false
      },
      fixed: {
        type: Boolean,
        default: false
      }
    },
    data: () => {
      return {
        users: [],
        fields: [
          {key: 'id'},
          {key: 'name'},
          {key: 'username'},
          {key: 'email'},
          {key: 'phone'},
          {key: 'website'},
          {key: 'company.name'}
        ],
        currentPage: 1,
        perPage: 5,
        totalRows: 0,
        search: ""
      }
    },
    // Get user info when the page is created
    created() {
      this.getUserInfo();
    },
    computed: {
      filteredList() {
        return this.users.filter(user => {
          // search in user while typing
          return user.name.toLowerCase().includes(this.search.toLowerCase());
        })
      }
    },
    methods: {
      // fetch api data
      getUserInfo() {
        this.axios.get('https://jsonplaceholder.typicode.com/users')
          .then((res) => {
            this.users = res.data;
          })
          .catch(error => {
            console.log(error.response)
          });
      },
      getRowCount(users) {
        return users.length
      },
      userLink(id) {
        return `users/${id.toString()}`
      },
      rowClicked(user) {
        const userLink = this.userLink(user.id)
        this.$router.push({path: userLink})
      }
    }
  }
</script>

<style scoped>
  .card-body >>> table > tbody > tr > td {
    cursor: pointer;
  }
</style>
