<template>
  <div class="container">
    <h2>Users</h2>
    <ul class="users">
      <li>
        <nuxt-link :to="'/users/'+users.id">{{ users.title }}</nuxt-link>
      </li>
    </ul>
  </div>
</template>

<script>
  import axios from 'axios'
  export default {
    validate ({ params }) {
      return !isNaN(+params.id)
    },
    asyncData ({ params, error }) {
      return axios.get(`http://www.kaiyaoservice.com:8091/getProjectByID/${+params.id}`)
          .then((res) => {
            return { users: res.data }
          })
          .catch(() => {
            error({ message: 'User not found', statusCode: 404 })
          })
    }
  }
</script>

<style scoped>
  .container {
    text-align: center;
    margin-top: 100px;
    font-family: sans-serif;
  }
  .users {
    list-style-type: none;
  }
  .users li a {
    display: inline-block;
    width: 200px;
    border: 1px #ddd solid;
    padding: 10px;
    text-align: left;
    color: #222;
    text-decoration: none;
  }
  .users li a:hover {
    color: orange;
  }
</style>
