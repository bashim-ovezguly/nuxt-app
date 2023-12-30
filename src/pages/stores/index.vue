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


        <div v-if="fetchFail == false" class="home">
            <h1 class="text-3xl font-bold p-[10px]">Dükanlar</h1>
            <div
                class="flex"
            >
                <input
                    v-model="searchName"
                    type="search"
                    class="border rounded mx-[5px] px-[10px] p-[0px] m-[0px] text-[13px]"
                    placeholder="Ady boýunça gözleg..."
                />
                <button @click="setData()">
                    <IconSearch
                        class="text-slate-400 hover:bg-slate-100 rounded  w-[30px] h-[30px]"
                    >
                    </IconSearch>
                </button>
            </div>
        </div>

        <h3 v-if="items.length == 0 && !isLoading">Dükan tapylmady</h3>

        <MyLoader v-if="isLoading"></MyLoader>

        <div class="flex flex-wrap items justify-center">
            <div
                v-for="(item, i) in items"
                :key="i"
                class="item grid shadow-md rounded-lg overflow-hidden border m-[10px] w-[230px]"
            >
                <NuxtLink
                    class="w-[230px] h-230px"
                    :to="'stores/' + item.id + '/products'"
                >
                    <img
                        class="w-full object-cover h-60"
                        :src="server + item.img"
                    />
                </NuxtLink>

                <div class="text grid p-[10px]">
                    <label class="text-sky-400">
                        <label class="text-bold">{{ item.name }}</label>
                    </label>
                    <label class="text-[13px]">{{ item.location }}</label>
                </div>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
// @ is an alias to /src
import axios from 'axios'
import MyLoader from '@/components/MyLoader.vue'
import IconSearch from '@/components/icons/IconSearch.vue'

export default {
    name: 'StoresView',
    components: { MyLoader, IconSearch },

    data() {
        return {
            fetchFail: false,
            items: [],
            server: process.env.server_ip,
            searchName: '',
            isLoading: true,
        }
    },
    async fetch() {
        await axios
            .get(this.server + '/mob/stores?name=' + this.searchName)
            .then((resp) => {
                this.items = resp.data.data
                this.isLoading = false
            })
            .catch(() => {
                this.fetchFail = true
                this.isLoading = true
            })
    },

    methods: {
        setData() {
            this.isLoading = true

            axios
                .get(this.server + '/mob/stores?name=' + this.searchName)
                .then((resp) => {
                    this.items = resp.data.data
                    this.isLoading = false
                })
                .catch(() => {
                    this.fetchFail = true
                    this.isLoading = false
                })
        },
    },
}
</script>
