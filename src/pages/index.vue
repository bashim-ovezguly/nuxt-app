<template>
    <div class="content">
        <h1 class="text-3xl font-bold p-[10px]">Maslahat berilýän dükanlar</h1>

        <div class="flex flex-wrap items justify-center">
            <div
                v-for="(item, i) in items"
                :key="i"
                class="item grid shadow-md rounded-lg overflow-hidden border m-[10px] w-[230px]"
            >
                <NuxtLink :to="'stores/' + item.id + '/products'">
                    <img
                        class="w-full object-cover h-60"
                        :src="server + item.img"
                    />
                </NuxtLink>

                <div class="text grid p-[10px]">
                    <label class="text-sky-400">
                        <label>{{ item.name }}</label>
                    </label>
                    <div class="flex items-center">
                        <IconLoaction
                            class="text-slate-400 w-[15px] h-[15px]"
                        ></IconLoaction>
                        <label class="text-slate-400">{{
                            item.location
                        }}</label>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
// @ is an alias to /src
import axios from 'axios'
import IconLoaction from '../components/icons/IconLocation.vue'
import { serverIP } from '../utils/constants'
import NotificationSuccess from '~/components/NotificationSuccess.vue'

export default {
    name: 'HomeView',
    components: { IconLoaction, NotificationSuccess },

    async asyncData() {
        try {
            const resp = await axios.get(serverIP + '/mob/stores?premium=1')
            return {
                items: resp.data.data,
                server: serverIP,
            }
        } catch (err) {
            alert('fetch error')
        }
    },
}
</script>
