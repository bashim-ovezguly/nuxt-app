<template>
    <div class="store-detail">
      
        <div class="store-header flex m-[10px] p-[5px]">
            <img
                class="border object-cover w-[200px] h-[200px] rounded-lg shadow-md "
                :src="server + store.img"
            />
            <div class="grid p-[20px] h-max">
                <h2 class="text-[30px] font-bold ">{{ store.name }}</h2>
                <h2 class="text-[20px]">{{ location.name }}</h2>
            </div>
        </div>

        <div class="tab  p-[10px] m-[10px] shadow-md rounded-lg overflow-hidden m-[10px] border">
            <a 
                class="p-[5px] text-sky-400 hover:bg-sky-400 hover:text-white m-[10px] rounded" 
                href="products">
                Harytlar
            </a>
            <a 
                class="p-[5px] text-sky-400 hover:bg-sky-400 hover:text-white m-[10px] rounded" 
                href="images">
                Suratlar
            </a>
            <a 
                class="p-[5px] text-sky-400 hover:bg-sky-400 hover:text-white m-[10px] rounded" 
                href="about">
                Dükan barada
            </a>
        </div>

        <div class="tab-content m-[10px]">
            <RouterView />
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
            server: process.env.server_ip,
        };
    },
    created() {
        this.id = this.$route.path.split("/")[2];
        axios
            .get( this.server+ "/mob/stores/" + this.id)
            .then((resp) => {
            this.store = resp.data;
            this.location = resp.data.location;
        });
        axios
            .get( this.server + "/mob/products?store=" + this.id)
            .then((resp) => {
            this.products = resp.data.data;
        });
    },
};
</script>

<style scoped>
    .tab{
        padding: 10px;
    }

    .tab-content-name{
        font-size: 20px;
        color: slategray;
        margin: 5px;
    }
</style>
