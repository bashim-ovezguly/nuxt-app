<template>
    <div class="content">
        <div v-if="fetchFail == true" class="grid justify-center">
            <h1 class="text-[25px] p-[10px]">Serwer jogap bermedi</h1>
            <Icon name="uil:github" color="black" />
            <button
                class="bg-gray-200 rounded shadow-md"
                onclick="this.fetch()"
            >
                Täzeden synanyşmak
            </button>
        </div>

        <h1 v-if="fetchFail == false" class="text-3xl font-bold p-[10px]">
            Maslahat berilýän dükanlar
        </h1>

        <MyLoader v-if="isLoading"></MyLoader>
        <div class="flex flex-wrap items justify-center">
            <div
                v-for="(item, i) in items"
                :key="i"
                class="item grid shadow-md rounded-lg overflow-hidden border m-[10px] w-[230px]"
            >
                <NuxtLink :to="'stores/' + item.id + '/products'">
                    <img
                        class="w-full object-cover h-60"
                        :src="server + item.img"
                    />
                </NuxtLink>

                <div class="text grid p-[10px]">
                    <label class="text-sky-400">
                        <label>{{ item.name }}</label>
                    </label>
                    <div class="flex items-center">
                        <IconLoaction
                            class="text-slate-400 w-[15px] h-[15px]"
                        ></IconLoaction>
                        <label class="text-slate-400">{{
                            item.location
                        }}</label>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
// @ is an alias to /src
import axios from 'axios'
import IconLoaction from '../components/icons/IconLocation.vue'
import MyLoader from '~/components/MyLoader.vue'

export default {
    name: 'HomeView',
    components: { IconLoaction, MyLoader },

    data() {
        return {
            fetchFail: false,
            items: [],
            server: process.env.server_ip,
            loginModal: false,
            isLoading:true,
        }
    },
    async fetch() {
        await axios
            .get(this.server + '/mob/stores?premium=1')
            .then((resp) => {
                this.items = resp.data.data
                this.isLoading = false
            })
            .catch(() => {
                this.fetchFail = true
                this.isLoading = false
            })
    },
}
</script>
