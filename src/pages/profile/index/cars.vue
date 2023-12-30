<template>
    <div>
        <h1 class="text-bold text-[20px] m-[10px] text-slate-500">
            Awtoulaglar {{ items.length }}
        </h1>
        <div class="flex flex-wrap items border p-[5px] m-[5px]">
            <div
                v-for="(item, i) in items"
                :key="i"
                class="item grid shadow-md rounded-lg overflow-hidden border m-[10px] w-[230px]"
            >
                <NuxtLink class="w-[230px] h-230px" :to="'/cars/' + item.id">
                    <img
                        class="w-full object-cover h-60"
                        :src="server_ip + item.img"
                    />
                </NuxtLink>

                <div class="text grid p-[10px]">
                    <label class="text-sky-400">
                        <label>{{ item.name }}</label>
                    </label>
                    <label>{{ item.location }}</label>
                    <label>{{ item.price }}</label>
                </div>
            </div>
        </div>
        <div class="images">
            <!-- <img :src="server_ip + img.img_m" v-for="img in images"> -->
        </div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    data() {
        return {
            items: [],
            images: [],
            server_ip: process.env.server_ip,
            user_id: this.$cookies.get('user_id'),
        }
    },

    async fetch() {
        await axios
            .get(this.server_ip + '/mob/cars?customer=' + this.user_id)
            .then((resp) => {
                this.items = resp.data.data
                this.images = resp.data.data.images
            })
            .catch(() => {
                this.fetchFail = true
            })
    },
}
</script>
