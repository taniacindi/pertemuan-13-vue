<template>
  <div class="container">
    <h1>Tambah User</h1>

    <form @submit.prevent="createUser">

      <div class="form-group">
        <label>Nama</label>
        <input
          type="text"
          v-model="name"
          placeholder="Masukkan nama"
          required
        />
      </div>

      <div class="form-group">
        <label>Pekerjaan</label>
        <input
          type="text"
          v-model="job"
          placeholder="Masukkan pekerjaan"
          required
        />
      </div>

      <button type="submit">
        Simpan
      </button>

      <router-link to="/">
        <button type="button">
          Kembali
        </button>
      </router-link>

    </form>

    <div v-if="hasil">
      <hr>

      <h3>Data Berhasil Ditambahkan</h3>

      <p><b>ID :</b> {{ hasil.id }}</p>
      <p><b>Nama :</b> {{ hasil.name }}</p>
      <p><b>Pekerjaan :</b> {{ hasil.job }}</p>
    </div>

  </div>
</template>

<script setup>
import { ref } from 'vue'
import axios from 'axios'

const name = ref('')
const job = ref('')
const hasil = ref(null)

const createUser = async () => {
  try {
    const response = await axios.post(
      'https://reqres.in/api/users',
      {
        name: name.value,
        job: job.value
      },
      {
        headers: {
          'x-api-key': 'reqres_36a805502b834ca9b200a4591fe8fb15'
        }
      }
    )

    hasil.value = response.data

    alert('User berhasil ditambahkan')

  } catch (error) {
    console.log(error)
    alert('Gagal menambahkan user')
  }
}
</script>

<style scoped>
.container{
    width:600px;
    margin:auto;
    margin-top:30px;
}

.form-group{
    margin-bottom:15px;
}

input{
    width:100%;
    padding:10px;
}

button{
    padding:10px 20px;
    margin-right:10px;
}
</style>