<template>
    <div>
        <NotificationSuccess
            v-if="notifSuccessLogin"
            :message="'Siz üstünlikli ulgama girdiňiz!'"
        ></NotificationSuccess>

        <div class="grid h-max">
            <div class="flex h-max m-[30px] p-[10px] w-max h-max min-w-[600px]">
                <img
                    :src="server_ip + userPhoto"
                    class="w-[150px] h-[150px] [m-10px] rounded-[10px] object-cover"
                />
                <div class="grid px-[10px]">
                    <label class="text-[25px] text-bold">{{ name }}</label>
                    <label class="text-[20px] text-bold"
                        >+993 {{ username }}</label
                    >
                    <label class="text-[13px] text-slate-400 text-bold"
                        >Soňky gezek ulgamda: {{ lastlogin }}</label
                    ><label class="text-[30px] text-bold">{{ email }}</label>
                    <div>
                        <button
                            class="m-[5px] p-[5px] rounded text-sky-400 hover:text-slate-500"
                            @click="logout"
                        >
                            Çykmak
                        </button>
                        <button></button>
                    </div>
                </div>
            </div>
            <div class="tab flex h-max max-w-[600px]">
                <NuxtLink
                    class="m-[5px] p-[5px] rounded-[5px] text-slate-500 hover:text-sky-400"
                    to="products"
                >
                    Harytlar
                </NuxtLink>
                <NuxtLink
                    class="m-[5px] p-[5px] text-slate-500 hover:text-sky-400"
                    to="cars"
                >
                    Awtoulaglar</NuxtLink
                >
                <NuxtLink
                    class="m-[5px] p-[5px] text-slate-500 hover:text-sky-400"
                    to="parts"
                >
                    Awtoşaýlar
                </NuxtLink>
            </div>
            <div class="tab-content m-[10px]">
                <RouterView />
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import { serverIP } from '@/utils/constants'
import NotificationSuccess from '~/components/NotificationSuccess.vue'

export default {
    components: { NotificationSuccess },

    async asyncData({ $cookies }) {
        const userId = $cookies.get('user_id')
        try {
            const resp = await axios.get(
                process.env.server_ip + '/mob/customer/' + userId,
            )
            return {
                userPhoto: resp.data.data.img,
                lastlogin: resp.data.data.last_login,
                email: resp.data.data.email,
                username: resp.data.data.phone,
                name: resp.data.data.name,
                server_ip: serverIP,
            }
        } catch (err) {
            alert('fetch error')
        }
    },

    data() {
        return {
            notifSuccessLogin: this.$cookies.get('notifSuccessLogin'),
        }
    },

    mounted() {
        this.$cookies.set('notifSuccessLogin', false)
    },
    // created(){
    //     this.$cookies.set('notifSuccessLogin', false);
    // },

    methods: {
        logout() {
            this.$cookies.removeAll()
            window.location.href = '/'
        },
    },
}
</script>
