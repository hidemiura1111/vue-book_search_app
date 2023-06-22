<template>
  <div>
    Book Edit
    {{ books }}
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
  }

}
</script>

<style>

</style>