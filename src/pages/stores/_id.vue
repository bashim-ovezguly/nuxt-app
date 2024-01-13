<template>
    <div class="store-detail">
        <div class="store-header flex m-[10px] p-[5px]">
            <img
                class="border object-cover w-[200px] h-[200px] rounded-lg shadow-md"
                :src="server + store.img"
            />
            <div class="grid p-[20px] h-max">
                <h2 class="text-[30px] font-bold">{{ store.name }}</h2>
                <h2 class="text-[20px]">{{ location.name }}</h2>
            </div>
        </div>

        <div
            class="tab p-[10px] m-[10px] shadow-md rounded-lg overflow-hidden m-[10px] border"
        >
            <NuxtLink
                class="p-[5px] text-sky-400 hover:bg-sky-400 hover:text-white m-[10px] rounded"
                to="products"
            >
                Harytlar
            </NuxtLink>
            <NuxtLink
                class="p-[5px] text-sky-400 hover:bg-sky-400 hover:text-white m-[10px] rounded"
                to="cars"
            >
                Awtoulaglar
            </NuxtLink>
            <NuxtLink
                class="p-[5px] text-sky-400 hover:bg-sky-400 hover:text-white m-[10px] rounded"
                to="images"
            >
                Suratlar
            </NuxtLink>
            <NuxtLink
                class="p-[5px] text-sky-400 hover:bg-sky-400 hover:text-white m-[10px] rounded"
                to="about"
            >
                Dükan barada
            </NuxtLink>
        </div>

        <div class="tab-content m-[10px]">
            <RouterView />
        </div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    async asyncData({ params }) {
        const storeId = params.id

        try {
            const resps = await Promise.all([
                axios.get(process.env.server_ip + '/mob/stores/' + storeId),
                axios.get(
                    process.env.server_ip + '/mob/products?store=' + storeId,
                ),
            ])
            return {
                store: resps[0].data,
                location: resps[0].data.location,
                products: resps[1].data.data,
            }
        } catch (err) {
            alert('fetch error')
        }
    },

    data() {
        return {
            name: '',
            location: '',
            id: '',
            store: '',
            server: process.env.server_ip,
            fetchFail: true,
        }
    },
}
</script>

<style scoped>
.tab {
    padding: 10px;
}

.tab-content-name {
    font-size: 20px;
    color: slategray;
    margin: 5px;
}
</style>
