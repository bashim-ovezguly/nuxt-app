<template>
    <div class="products">
        <label class="tab-content-name">Awtoulaglar: {{ productsCount }}</label>
        <div class="flex flex-wrap justify-center">
            <div
                v-for="product in products"
                :key="product.id"
                class="grid w-max-content h-80 m-5 shadow-md rounded-lg overflow-hidden border"
            >
                <NuxtLink :to="'/cars/' + product.id">
                    <img
                        class="object-cover w-[230px] h-[230px]"
                        :src="server + product.img"
                    />
                </NuxtLink>

                <div class="p-[10px] grid border">
                    <label class="bg-white"
                        >{{ product.mark }} {{ product.model }}
                        {{ product.year }}</label
                    >
                    <label
                        class="bg-sky-700 text-white w-max p-[4px] h-max rounded-md"
                        >{{ product.price }}</label
                    >
                </div>
            </div>
        </div>
        <div v-if="loading == true">
            <label>Loading...</label>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'HomeView',
    data() {
        return {
            description: '',
            productsCount: 0,
            loading: true,
            items: [],
            server: process.env.server_ip,
            products: [],
        }
    },

    async fetch() {
        this.id = this.$route.params.id
        await axios
            .get(this.server + '/mob/cars?store=' + this.id)
            .then((resp) => {
                this.products = resp.data.data
                this.productsCount = resp.data.data.length
                this.loading = false
            })
    },

    head() {
        return {
            title: 'Awtoulaglar',
        }
    },
}
</script>
