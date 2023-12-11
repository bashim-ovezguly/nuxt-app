<template>
    <div>
        <div class="home">
        <h1 class="text-3xl font-bold">Stores</h1>
    </div>
    <div class="flex flex-wrap items justify-center">
        <div
            :key="id"
            v-for="(id, name, img) in items"
            class="grid w-60 h-80 m-5 shadow-md rounded-lg overflow-hidden"
        >
            <img class="w-full object-cover h-60" :src="server + {img}" />
            
            <a :href="'stores/' + id" class="text-sky-400" :to="'stores/' + id"
                ><label>{{ name }}</label></a>
            <!-- <label>{{ location }}</label> -->
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
            server: process.env.VUE_APP_BACKEND_ADDRESS,
        };
    },
    created() {
        axios
            .get( this.server+ "/mob/stores?premium=1")
            .then((resp) => {
                this.items = resp.data.data;
            });
    },
};
</script>
