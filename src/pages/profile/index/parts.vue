<template>
    <div>
        <h1 class="text-bold text-[20px] m-[10px] text-slate-500">
            Awtoşaýlar {{ items.length }}
        </h1>
        <div class="flex flex-wrap items border p-[5px] m-[5px]">
            <div
                v-for="(item, i) in items"
                :key="i"
                class="item grid shadow-md rounded-lg overflow-hidden border m-[10px] w-[230px]"
            >
                <NuxtLink class="w-[230px] h-230px" :to="'/parts/' + item.id">
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
    </div>
</template>

<script>
import axios from 'axios'
import { serverIP } from '@/utils/constants'

export default {
    async asyncData({ $cookies }) {
        const userId = $cookies.get('user_id')
        try {
            const resp = await axios.get(
                process.env.server_ip + '/mob/parts?customer=' + userId,
            )
            return {
                items: resp.data.data,
            }
        } catch (err) {
            alert('fetch error')
        }
    },

    data() {
        return {
            items: [],
            server_ip: serverIP,
            user_id: this.$cookies.get('user_id'),
        }
    },
}
</script>
