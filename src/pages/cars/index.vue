<template>
    <div class="content">
        <div v-if="fetchFail == false" class="home">
            <h1 class="text-3xl font-bold p-[10px]">Awtoulaglar</h1>
            <div>
                <input
                    v-model="searchName"
                    class="border rounded mx-[5px] px-[5px]"
                    placeholder="Ady boýunça gözleg..."
                />
            </div>
        </div>
        <div class="flex flex-wrap items justify-center">
            <div
                v-for="(item, i) in items"
                :key="i"
                class="item grid shadow-md rounded-lg overflow-hidden border m-[10px] w-[230px]"
            >
                <NuxtLink class="w-[230px] h-230px" :to="'cars/' + item.id">
                    <img
                        class="w-full object-cover h-60"
                        :src="server + item.img"
                    />
                </NuxtLink>

                <div class="text grid p-[10px]">
                    <label class="text-sky-400">
                        <label
                            >{{ item.mark }} {{ item.model }}
                            {{ item.year }}</label
                        >
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
    name: 'Products',

    async asyncData() {
        try {
            const resp = await axios.get(process.env.server_ip + '/mob/cars')
            return { items: resp.data.data }
        } catch (err) {
            alert('fetch error')
        }
    },

    data() {
        return {
            fetchFail: false,
            items: [],
            server: process.env.server_ip,
            searchName: '',
        }
    },
}
</script>
