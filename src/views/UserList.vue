<template>
  <div class="container">
    <h1>Daftar User</h1>

    <router-link to="/create">
      <button>Tambah User</button>
    </router-link>

    <table>
      <thead>
        <tr>
          <th>ID</th>
          <th>Nama</th>
          <th>Email</th>
          <th>Aksi</th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="user in users" :key="user.id">
          <td>{{ user.id }}</td>
          <td>{{ user.first_name }} {{ user.last_name }}</td>
          <td>{{ user.email }}</td>
          <td>
            <router-link :to="'/detail/' + user.id">
              Detail
            </router-link>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'

const users = ref([])

const getUsers = async () => {
  try {
    const response = await axios.get(
      'https://reqres.in/api/users?page=1',
      {
        headers: {
          'x-api-key': 'reqres_36a805502b834ca9b200a4591fe8fb15'
        }
      }
    )

    users.value = response.data.data
  } catch (error) {
    console.log(error)
  }
}

onMounted(() => {
  getUsers()
})
</script>

<style scoped>
.container{
    width:900px;
    margin:auto;
    margin-top:30px;
}

table{
    width:100%;
    border-collapse:collapse;
}

th,td{
    border:1px solid #ccc;
    padding:10px;
}

button{
    margin-bottom:15px;
    padding:8px 15px;
}
</style>