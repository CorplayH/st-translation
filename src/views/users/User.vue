<template>
  <b-row>
    <b-col cols="12" xl="12">
      <transition name="slide">
        <b-card>
          <div slot="header" v-html="caption"></div>
          <b-table :hover="hover" :striped="striped" :bordered="bordered" :small="small" :fixed="fixed" responsive="sm" :items="items" :fields="fields" :current-page="currentPage"
                   :per-page="perPage" @row-clicked="rowClicked">
            <template slot="id" slot-scope="data">
              <strong>{{data.item.title}}</strong>
            </template>
          </b-table>
          <template slot="footer">
          <b-button @click="goBack">Back</b-button>
          </template>
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
        default: 'Article'
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
          {key: 'title'},
        ],
        currentPage: 1,
        perPage: 10,
        totalRows: 0
      }
    },
    // Get user info when the page is created
    created() {
      this.getUserInfo();
    },
    methods: {
      // fetch user data
      getUserInfo() {
        this.axios.get('https://jsonplaceholder.typicode.com/posts?userId=' + this.$route.params.id)
          .then((res) => {
            this.items = res.data;
          })
          .catch(error => {
            console.log(error.response)
          });
      },
      // pagination functions
      getRowCount(items) {
        return items.length
      },
      articleLink(id) {
        return `/article/${id.toString()}`
      },
      rowClicked(item) {
        const articleLink = this.articleLink(item.id)
        this.$router.push({path: articleLink})
      },
      goBack() {
        this.$router.go(-1)
        // this.$router.replace({path: '/users'})
      }
    }
  }
</script>
<style scoped>
  .card-body >>> table > tbody > tr > td {
    cursor: pointer;
  }
</style>
