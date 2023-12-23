<template>
  <div class="content">
    <div v-if="fetchFail == true" class="grid justify-center">
      <h1 class="text-[25px] p-[10px]">Serwer jogap bermedi</h1>
      <Icon name="uil:github" color="black" />
      <button class="bg-gray-200 rounded shadow-md" onclick="this.fetch()">
        Täzeden synanyşmak
      </button>
    </div>

    <div v-if="fetchFail == false" class="home">
      <h1 class="text-3xl font-bold p-[10px]">Dükanlar</h1>
      <div class="search flex border rounded max-w-[200px] p-[5px] m-[10px]">
        <input v-bind="searchName" placeholder="Ady boýunça gözleg..." />
      </div>
    </div>
    <div class="flex flex-wrap items justify-center">
      <div
        v-for="(item, i) in items"
        :key="i"
        class="item grid shadow-md rounded-lg overflow-hidden border m-[10px] w-[230px]"
      >
        <a class="w-[230px] h-230px" :href="'products/' + item.id">
          <img class="w-full object-cover h-60" :src="server + item.img" />
        </a>

        <div class="text grid p-[10px]">
          <label class="text-sky-400">
            <label>{{ item.name }}</label>
          </label>
          <label>{{ item.location }}</label>
          <label>{{ item.price }}</label>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
// @ is an alias to /src
import axios from 'axios'

export default {
  StoreCard: {
    name: String,
    location: String,
  },
  name: 'Products',
  data() {
    return {
      fetchFail: false,
      items: [],
      server: process.env.server_ip,
      searchName: '',
    }
  },
  async fetch() {
    await axios
      .get(this.server + '/mob/products')
      .then((resp) => {
        this.items = resp.data.data
      })
      .catch(() => {
        this.fetchFail = true
      })
  },
}
</script>
