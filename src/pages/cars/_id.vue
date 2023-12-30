<template>
    <div class="store-detail">
        <div class="store-header flex m-[10px] p-[5px]">
            <img
                class="border object-cover w-[500px] h-[500px] rounded-lg shadow-md"
                :src="server + img"
            />
            <div class="grid p-[20px] h-max">
                <h2 class="text-[30px] font-bold">
                    {{ mark }} {{ model }} {{ year }}
                </h2>
                <h2 class="text-[20px]">{{ description }}</h2>
                <h3 class="text-[20px]">{{ price }}</h3>
                <h3 class="text-[20px]">{{ category }}</h3>
                <h3 class="text-[20px]">{{ location }}</h3>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    data() {
        return {
            name: '',
            price: '',
            location: '',
            id: '',
            store: '',
            server: process.env.server_ip,
            fetchFail: true,
        }
    },

    async fetch() {
        this.id = this.$route.params.id
        try {
            const resps = await Promise.all([
                axios.get(this.server + '/mob/cars/' + this.id),
            ])
            this.price = resps[0].data.price
            this.description = resps[0].data.description
            this.location = resps[0].data.location
            this.img = resps[0].data.img
            this.mark = resps[0].data.mark
            this.model = resps[0].data.model
            this.year = resps[0].data.year
            this.img = resps[0].data.img.img_m
        } catch (err) {
            this.fetchFail = true
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
