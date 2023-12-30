<script>
import axios from 'axios'

export default {
    data() {
        return {
            username: '',
            password: '',
            server_ip: process.env.server_ip,
        }
    },

    methods: {
        loginClick() {
            localStorage.clear()
            const formdata = new FormData()
            formdata.append('phone', this.username)
            formdata.append('password', this.password)

            axios
                .post(this.server_ip + '/mob/token/obtain', formdata)
                .then((resp) => {
                    document.location.href = '/profile/products'
                    this.$cookies.removeAll()
                    this.$cookies.set('phone', resp.data.data.phone)
                    this.$cookies.set('user_id', resp.data.data.id)
                    this.$cookies.set('name', resp.data.data.name)
                    this.$cookies.set(
                        'access_token',
                        resp.data.data.access_token,
                    )
                    this.$cookies.set(
                        'refresh_token',
                        resp.data.data.refresh_token,
                    )
                })
                .catch(() => {
                    alert('Invalid username or password')
                })
        },
    },
}
</script>

<template>
    <div class="bgk">
        <div
            class="fields grid w-400px h-max shadow-md rounded-[10px] p-[20px] border"
        >
            <label class="text-[30px] text-sky-400 text-bold my-[10px]"
                >Giriş</label
            >
            <label class="text-[12px] mt-[5px]">Ulanyjy adyňyz</label>
            <input v-model="username" type="username" class="border rounded" />
            <label class="text-[12px] mt-[5px]">Açar sözüňiz</label>
            <input v-model="password" type="password" class="border rounded" />
            <button
                class="rounded bg-sky-400 text-white p-[2px] my-[5px] text-[14px]"
                @click="loginClick"
            >
                Içeri girmek
            </button>
            <button
                class="rounded bg-sky-400 text-white p-[2px] my-[5px] text-[14px]"
            >
                Registrasiýa
            </button>
        </div>
    </div>
</template>

<style>
.bgk {
    display: flex;
    justify-content: center;
}

.fields {
    background: white;
    min-width: 300px;
    margin-top: 5%;
}
</style>
