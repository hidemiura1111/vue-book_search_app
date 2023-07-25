<template>
  <v-footer
    color="primary"
    dark
  >
    <v-row
      justify="center"
      no-gutters
    >
      <v-col
        class="primary py-4 text-center white--text"
        cols="12"
      >
        {{ new Date().getFullYear() }} — <strong>Book Search App</strong>
      </v-col>
    </v-row>
  </v-footer>
</template>

<script>
export default {
  name: 'FooterComponent',
}
</script>

<style>

</style>