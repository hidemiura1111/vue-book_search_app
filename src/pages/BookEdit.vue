<template>
  <div>
    Book Edit
    <!-- {{ book.title }} -->
    {{ books[this.$route.params.id - 1].title }}
    <!-- {{ books }} -->
  </div>
</template>

<script>
export default {
  name: 'BookEdit',
  props: {
    books: {
      type: Array,
      required: false,
    },
  },
  data() {
    return {
      book: ''
    }
  },
  // beforeRouteEnter(to, from, next) {
  //   next(vm => {
  //     vm.$nextTick(() => {
  //       console.log(vm.books);
  //       console.log(vm.$route.params.id);
  //       vm.book = vm.books[vm.$route.params.id];
  //       console.log(vm.book);
  //     });
  //   });
  // }
  
  // created() {
  //   this.fetchData();
  // },
  // methods: {
  //   fetchData() {
  //     console.log(this.books);
  //     console.log(this.$route.params.id);
  //     this.book = this.books[this.$route.params.id - 1];
  //     console.log(this.book);
  //   }
  // }

}
</script>

<style>

</style>