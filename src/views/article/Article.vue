<template>
  <div class="animated fadeIn">
    <b-row>
      <b-col sm="12" md="12">
        <b-card :header="article.body" border-variant="warning">
          {{article.body}}
        </b-card>
      </b-col>
    </b-row>

    <b-button @click="goBack">Back</b-button>

  </div>

</template>
<script>
  export default {
    name: "userArticle",
    data: function () {
      return {
        article: {}
      }
    },
    created() {
      this.getArticle();
    },
    methods: {
      // fetch api data
      getArticle() {
        this.axios.get('https://jsonplaceholder.typicode.com/posts/' + this.$route.params.id)
          .then((res) => {
            this.article = res.data;
          })
          .catch(error => {
            console.log(error.response)
          });
      },
      goBack() {
        this.$router.go(-1)
      }
    }
  }

</script>

<style scoped>
  .fade-enter-active {
    transition: all .3s ease;
  }
  .fade-leave-active {
    transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
  }
  .fade-enter, .fade-leave-to {
    transform: translateX(10px);
    opacity: 0;
  }
</style>
