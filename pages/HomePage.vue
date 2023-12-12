<template>
    <div>
        <Header></Header>
        <div class="home">
            <h1 class="text-3xl font-bold">Premium stores</h1>
        </div>
        <div class="flex flex-wrap items justify-center">
            <div
                v-for="(item, i) in items"
                :key="i"
                class="item grid w-60 h-80 m-5 shadow-md rounded-lg overflow-hidden"
            >
                <img class="w-full object-cover h-60" :src="server + item.img" />
                
                <a :href="'stores/' + item.id" class="text-sky-400" :to="'stores/' + item.id"
                    ><label>{{item.name }}</label></a>
                <label>{{ item.location }}</label>
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
            server: 'http://216.250.9.45:8000',
        };
    },
    created() {

        axios
            .get( this.server + "/mob/stores?premium=1")
            .then((resp) => {
                this.items = resp.data.data;
            });
    },
};
</script>
