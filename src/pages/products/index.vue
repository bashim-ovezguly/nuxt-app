<template>
    <div class="content">
        <div v-if="fetchFail == false" class="home">
            <h1 class="text-3xl font-bold p-[10px]">Harytlar</h1>
            <div class="flex items-center">
                <input
                    v-model="searchName"
                    type="search"
                    class="border rounded mx-[5px] p-[5px] text-[13px]"
                    placeholder="Ady boýunça gözleg..."
                />

                <button @click="setData()">
                    <IconSearch
                        class="text-slate-400 hover:bg-slate-100 rounded w-[30px] h-[30px]"
                    >
                    </IconSearch>
                </button>
            </div>
        </div>

        <div class="flex flex-wrap items justify-center">
            <div
                v-for="(item, i) in items"
                :key="i"
                class="item grid shadow-md rounded-lg overflow-hidden border m-[10px] w-[230px]"
            >
                <a class="w-[230px] h-230px" :href="'products/' + item.id">
                    <img
                        class="w-full object-cover h-60"
                        :src="server + item.img"
                    />
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
import IconSearch from '@/components/icons/IconSearch.vue'
import { serverIP } from '@/utils/constants'

export default {
    StoreCard: {
        name: String,
        location: String,
    },
    components: { IconSearch },

    async asyncData() {
        try {
            const resp = await axios.get(
                process.env.server_ip + '/mob/products',
            )
            return { items: resp.data.data }
        } catch (err) {
            alert('fetch error')
        }
    },

    data() {
        return {
            fetchFail: false,
            items: [],
            server: serverIP,
            searchName: '',
            isLoading: true,
        }
    },

    methods: {
        setData() {
            axios
                .get(this.server + '/mob/products?name=' + this.searchName)
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
