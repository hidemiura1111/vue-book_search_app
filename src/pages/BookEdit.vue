<template>
  <div>
    Book Edit
    {{ book?.title }}
    <!-- {{ books[this.$route.params.id - 1].title }} -->
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
  watch: {
    books: {
      immediate: true,
      handler() {
        this.book = this.books[this.$route.params.id - 1];
      }
    }
  }
  // beforeRouteEnter (to, from, next) {
  //   next(vm => {
  //     vm.$nextTick(() => {
  //       console.log(vm.books);
  //       vm.book = vm.books[vm.$route.params.id - 1];
  //     });
  //   });
  // }
}
</script>

<style>

</style>