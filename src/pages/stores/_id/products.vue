<template>
    <div class="products">
        <label class="tab-content-name">Harytlar: {{ productsCount }}</label>
        <div class="flex flex-wrap justify-center">
            <div
                v-for="product in products"
                :key="product.id"
                class="grid w-max-content h-80 m-5 shadow-md rounded-lg overflow-hidden border"
            >
                <a :href="'/products/' + product.id">
                    <img
                        class="object-cover w-[230px] h-[230px]"
                        :src="server + product.img"
                    />
                </a>

                <div class="p-[10px]">
                    <label class="bg-white">{{ product.name }}</label>
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
            .get(this.server + '/mob/products?store=' + this.id)
            .then((resp) => {
                this.products = resp.data.data
                this.productsCount = resp.data.data.length
                this.loading = false
            })
    },

    head() {
        return {
            title: 'Harytlar',
        }
    },
}
</script>
