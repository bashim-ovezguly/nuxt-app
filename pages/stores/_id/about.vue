<template>
    <div class="about">
        <span style="white-space: pre-line">{{ description }}</span>
    </div>
</template>

<script>

import axios from "axios";
export default {
    name: "HomeView",
    data() {
        return {
            description:'',
            id:'',
            items: [],
            server: process.env.server_ip,
        };
    },
    created() {
        this.id = this.$route.path.split("/")[2];
        axios
            .get( this.server+ "/mob/stores/" + this.id)
            .then((resp) => {
            this.description = resp.data.body_tm;
        });
        
    },
};

</script>