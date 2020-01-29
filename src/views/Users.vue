<template>
  <div>
  <h1>User List</h1>

  <v-layout v-if="errored">
    <p>We're sorry, we're not able to retrieve this information at the moment, please try back later</p>
  </v-layout>

  <v-layout v-else>
    <div v-if="loading">Loading...</div>

    <v-data-table
      v-else
      :headers="headers"
      :items="users"
      :items-per-page="5"
      class="elevation-1"
      :loading="loading" loading-text="Loading... Please wait"
    >
      <template v-slot:item.avatar="{ item }">
        <img height="30" :src="item.avatar" />
      </template>
    </v-data-table>
  </v-layout>
</div>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      users: null,
      loading: true,
      errored: false,
      headers: [
        {
          text: 'Id',
          align: 'left',
          value: 'id',
        },
        { text: 'First Name', value: 'first_name' },
        { text: 'Last Name', value: 'last_name' },
        { text: 'Email Address', value: 'email' },
        { text: 'Avatar', value: 'avatar', sortable: false, justify: 'center' }
      ]
    }
  },
  filters: {
    currencydecimal (value) {
      return value.toFixed(2)
    }
  },
  mounted () {
    axios
      .get('https://reqres.in/api/users')
      .then(response => {
        this.users = response.data.data
      })
      .catch(error => {
        console.log(error)
        this.errored = true
      })
      .finally(() => this.loading = false)
  }
}
</script>
