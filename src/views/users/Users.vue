<template>
  <b-row>
    <b-col cols="12" xl="12">
      <transition name="slide">
        <b-card>
          <div slot="header" v-html="caption"></div>
          <b-table :hover="hover" :striped="striped" :bordered="bordered" :small="small" :fixed="fixed" responsive="sm" :items="items" :fields="fields" :current-page="currentPage"
                   :per-page="perPage" @row-clicked="rowClicked">
            <template slot="id" slot-scope="data">
              <strong>{{data.item.id}}</strong>
            </template>
            <template slot="name" slot-scope="data">
              <strong>{{data.item.name}}</strong>
            </template>
            <template slot="status" slot-scope="data">
              <b-badge :variant="getBadge(data.item.status)">{{data.item.status}}</b-badge>
            </template>
          </b-table>
          <nav>
            <b-pagination size="md" :total-rows="getRowCount(items)" :per-page="perPage" v-model="currentPage" prev-text="Prev" next-text="Next" hide-goto-end-buttons/>
          </nav>
        </b-card>
      </transition>
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
        items: [],
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
        totalRows: 0
      }
    },
    // Get user info when the page is created
    created() {
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

      getRowCount(items) {
        return items.length
      },
      userLink(id) {
        return `users/${id.toString()}`
      },
      rowClicked(item) {
        const userLink = this.userLink(item.id)
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
