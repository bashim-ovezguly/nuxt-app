<template>
    <div class="content">

        <div class="home">
            <h1 class="text-3xl font-bold p-[10px]">Premium stores</h1>
        </div>
        <div class="flex flex-wrap items justify-center">
            <div
                v-for="(item, i) in items"
                :key="i"
                class="item grid shadow-md rounded-lg overflow-hidden border m-[10px]"
                >
                <a class="w-[230px] h-230px" :href="'stores/' + item.id + '/products'" >
                    <img class="w-full object-cover h-60" :src="server + item.img" />
                </a>
                
                <div class="text grid p-[10px]">
                    <label class="text-sky-400" >
                        <label>{{item.name }}</label>
                    </label>
                    <label>{{ item.location }}</label>
                </div>
            </div>
        </div>
    </div>
  
</template>

<script lang="ts">
// @ is an alias to /src
import axios from "axios";

export default {
    name: "HomeView",
    data() {
        return {
            items: [],
            server: process.env.server_ip,

        };
    },
    async fetch() {
        await axios
            .get(this.server + "/mob/stores")
            .then((resp) => {
            this.items = resp.data.data;
        });
  },    
};
</script>

<style scoped>
    .item {
        display: grid;
    }
</style>
