<template>
    <div class="content">
        <div class="home">
            <h1 class="text-3xl font-bold p-[10px]">Dükanlar</h1>
            <div class="flex">
                <input
                    ref="search"
                    v-model="searchName"
                    type="search"
                    class="border rounded mx-[5px] px-[10px] p-[0px] m-[0px] text-[13px]"
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

        <h3 v-if="items.length == 0 && !isLoading">Dükan tapylmady</h3>

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
import IconSearch from '@/components/icons/IconSearch.vue'
import { serverIP } from '@/utils/constants'

export default {
    name: 'StoresView',
    components: { IconSearch },

    async asyncData() {
        try {
            const resp = await axios.get(
                process.env.server_ip + '/mob/stores?name=',
            )
            return { items: resp.data.data }
        } catch (err) {
            alert('fetch error')
        }
    },

    data() {
        return {
            items: [],
            server: serverIP,
            searchName: '',
            isLoading: true,
        }
    },

    methods: {
        setData() {
            axios
                .get(
                    this.server + '/mob/stores?name=' + this.$refs.search.value,
                )
                .then((resp) => {
                    this.items = resp.data.data
                    this.isLoading = false
                })
                .catch(() => {
                    this.isLoading = false
                })
        },
    },
}
</script>
