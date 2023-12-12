<template>
    <div class="storeDetail">
      
    </div>
</template>

<script>
// import axios from "axios";

export default {
    data() {
        
        return {
            name: "",
            location: "",
            id: "",
            store: "",
            products: [],
            server: 'http://216.250.9.45:8000'
        };
    },
    mounted() {
        this.id = this.$route.path.split("/")[3];
      
        axios
            .get( "http://216.250.9.45:8000/mob/products/" + this.id)
            .then((resp) => {
                this.products = resp.data.data;
            });
    },
};
</script>
