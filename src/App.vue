<template>
  <v-app>
    <HeaderComponent/>
      <v-main>
        <v-container>
          <router-view/>
        </v-container>
      </v-main>
    <FooterComponent/>
  </v-app>
</template>

<script>
import HeaderComponent from '@/global/HeaderComponent';
import FooterComponent from '@/global/FooterComponent';

export default {
  name: 'App',
  components: {
    HeaderComponent,
    FooterComponent,
  },
  data: () => ({
    //
  }),
};
</script>
