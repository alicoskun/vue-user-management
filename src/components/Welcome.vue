<template>
  <v-container>
    <v-layout
      text-center
      wrap
    >
      <v-flex xs12>
        <v-img
          :src="require('../assets/logo.svg')"
          class="my-3"
          contain
          height="50"
        ></v-img>
      </v-flex>

      <v-flex
        mb-5
        xs12
      >
        <h2 class="headline font-weight-bold mb-3">Pages</h2>
        <v-layout justify-center>
          
          <router-link 
            v-for="(page, i) in pages" 
            :key="i"
            :to="page.to"
            class="subheading mx-3"
          >
            {{ page.name }}
          </router-link>
        </v-layout>
      </v-flex>

    </v-layout>
    
    <v-layout justify-center>
      <router-view/>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  name: 'HelloWorld',

  data: () => ({
    pages: [
      {
        to: '/',
        name: 'Home',
      },
      {
        to: '/about',
        name: 'About',
      },
      {
        to: '/users',
        name: 'Users',
      },
    ],
  }),
};
</script>
