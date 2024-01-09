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

    async asyncData({params}) {
        const id = params.id
        try {
            const resps = await Promise.all([
                axios.get(process.env.server_ip + '/mob/cars/' + id),
            ])

            return {
                price : resps[0].data.price,
                description : resps[0].data.description,
                location : resps[0].data.location,
                mark : resps[0].data.mark,
                model : resps[0].data.model,
                year : resps[0].data.year,
                img : resps[0].data.img.img_m,
            }
            
        } catch (err) {
            alert('fetch error')
        }
    },

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
