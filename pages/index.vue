<template>
  <div class="h-screen bg-gray-50">
    <Home/>
    <div class="p-6" >
      <input class="p-3 rounded border border-gray-500 w-60 my-4 mx-auto " type="text" placeholder="search ">
      <button class="btn-blue">Clear Search</button>
    </div>
    <div class="bg-gray-100 p-8">
      <div class="grid md:grid-cols-2 gap-4 ">
        <div v-for="(siswa, id) in siswas" :key="id" class="border rounded px-3 py-2 shadow-md" >
          <div class="flex justify-between">
            <h1 class="text-lg font-semibold">{{siswa.namaSiswa}}</h1>
            <p>NIM :  {{siswa.nim}}</p>
          </div>
            <div class="flex justify-between mt-2">
              <p> Angkatan: {{siswa.angkatan}}</p>
              <p>Kelompok : {{siswa.namaKelompok}}</p>
            </div>
        </div>

      </div>

    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      siswas: [],
      searchedSiswa: [],
      error: null
    }
  },

    async mounted () {
      try {
        const response = await axios.get('http://localhost:1337/siswas')
        this.siswas = response.data
      } catch (error) {
        this.error = error;
      }
    }



  // async fetch() {
  //   await this.getSiswas()
  //   },

  //   methods: {
  //     async getSiswas() {
  //       const data = axios.get('http://localhost:1337/siswas')

  //       const result = await data
  //       result.data.results.forEach(siswa =>{
  //       this.siswas.push(siswa)
  //     });

  //     }
  //   }

  }
</script>

<style scoped>
  .btn-blue {
    @apply py-2 px-4 bg-blue-500 text-white font-semibold rounded-lg shadow-md hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-400 focus:ring-opacity-75;
  }
</style>
