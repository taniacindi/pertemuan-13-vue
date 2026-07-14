<template>
  <div class="container">
    <h1>Detail User</h1>

    <div v-if="user">
      <img :src="user.avatar" width="150" />

      <h2>{{ user.first_name }} {{ user.last_name }}</h2>

      <p>Email : {{ user.email }}</p>

      <router-link to="/">
        <button>Kembali</button>
      </router-link>
    </div>

    <div v-else>
      Loading...
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRoute } from 'vue-router'
import axios from 'axios'

const route = useRoute()

const user = ref(null)

const getUser = async () => {
  try {
    const response = await axios.get(
      `https://reqres.in/api/users/${route.params.id}`,
      {
        headers: {
          'x-api-key': 'reqres_36a805502b834ca9b200a4591fe8fb15'
        }
      }
    )

    user.value = response.data.data
  } catch (error) {
    console.log(error)
  }
}

onMounted(() => {
  getUser()
})
</script>

<style scoped>
.container{
    width:700px;
    margin:auto;
    text-align:center;
    margin-top:30px;
}

button{
    margin-top:20px;
    padding:10px 20px;
}
</style>