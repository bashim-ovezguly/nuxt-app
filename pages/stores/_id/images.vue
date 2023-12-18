<template>
    <div class="images">

        <label class="tab-content-name">Suratlar {{ imagesCount }}</label>
                <div class="flex flex-wrap justify-center">
                    <div 
                        v-for="item in images"
                        :key="item.id"
                        class="w-[230px] h-[230px] m-[10px] shadow-md rounded-lg overflow-hidden border"
                        >
                        <img
                            class="object-cover w-[230px] h-[230px]"
                            :src=" server + item.img_m"
                        />
                        
                    </div>
                </div>

   
    </div>

    
</template>

<script>

import axios from "axios";
export default {
    name: "HomeView",
    data() {
        return {
            description:'',
            imagesCount:0,
            loading:true,
            id:'',
            images: [],
            server: process.env.server_ip,
        };
    },
    async fetch() {
        this.id = this.$route.path.split("/")[2];
        await axios
            .get( this.server+ "/mob/stores/" + this.id)
            .then((resp) => {
            this.images = resp.data.images;
            this.imagesCount = resp.data.data.length
            this.loading = false;
        });
        
    },
    head() {
    return {
      title: "Suratlar"
    };
    },

};

</script>