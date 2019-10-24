<template>
  <div class="animated fadeIn">
    <b-row>
      <b-col sm="6" md="4">
        <b-card header="Card outline warning" border-variant="warning">
          Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat.
        </b-card>
      </b-col>
    </b-row>
  </div>
</template>
<script>
  export default {
    name: "details.vue",
    data: function () {
      return {
        show: true
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
