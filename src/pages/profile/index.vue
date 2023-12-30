<template>
    <div>
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

export default {
    data() {
        return {
            server_ip: process.env.server_ip,
            userPhoto: '',
            name: '',
            username: '',
            isLoading: '',
            user_id: this.$cookies.get('user_id'),
            email: '',
            lastlogin: '',
        }
    },

    created() {
        axios
            .get(this.server_ip + '/mob/customer/' + this.user_id)
            .then((resp) => {
                this.userPhoto = resp.data.data.img
                this.lastlogin = resp.data.data.last_login
                this.email = resp.data.data.email
                this.username = resp.data.data.phone
                this.name = resp.data.data.name
            })
            .catch(() => {
                this.fetchFail = true
                alert('fetch error')
            })
    },

    methods: {
        logout() {
            this.$cookies.removeAll()
            window.location.href = '/'
        },
    },
}
</script>
