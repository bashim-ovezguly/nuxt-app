<template>
    <div class="storeDetail">
        <a class="text-sky-400" href="/">Back to Stores</a>
        
        <h1>This is an store detail page</h1>
        <h2 class="font-bold text-xl">{{ store.name }}</h2>

        <div class="flex flex-wrap justify-center">
            <img
                class="max-w-xs rounded-lg shadow-md"
                :src="backend + store.img"
            />
        </div>

        <h2>{{ location.name }}</h2>
        <p>{{ store.description }}</p>
        <h2>{{ store.created_at }}</h2>

        <div v-if="products.length > 0">
            <h2>Products {{ products.length }}</h2>
            <div class="flex flex-wrap justify-center">
                <div
                    class="grid w-60 h-80 m-5 shadow-md rounded-lg overflow-hidden"
                    :key="product.id"
                    v-for="product in products"
                >
                    <img
                        class="object-cover w-full h-60"
                        :src=" backend + product.img"
                    />
                    <label>{{ product.name }}</label>
                </div>
            </div>
        </div>
        <div v-else>
            <h2>No products yet</h2>
        </div>
    </div>
</template>

<script>
import axios from "axios";

export default {
    data() {
        return {
            name: "",
            location: "",
            id: "",
            store: "",
            products: [],
            backend: process.env.VUE_APP_BACKEND_ADDRESS
        };
    },
    mounted() {
        this.id = this.$route.path.split("/")[2];
        axios
            .get( this.backend + "/mob/stores/" + this.id)
            .then((resp) => {
                this.store = resp.data;
                this.location = resp.data.location;
            });
        axios
            .get( this.backend + "/mob/products?store=" + this.id)
            .then((resp) => {
                this.products = resp.data.data;
            });
    },
};
</script>
