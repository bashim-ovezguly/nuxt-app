<template>
    <div class="shadow-md sticky top-[0px]">
        <div class="header flex p-[10px] justify-between">
            <NuxtLink to="/" class="flex">
                <img class="logo h-full" src="../static/logo_white.png" />
                <div class="text grid">
                    <label class="project-name"
                        >Söwda toplumy - MarketPlace</label
                    >
                </div>
            </NuxtLink>
            <div class="btns flex items-center">
                <div
                    class="hover:text-sky-500 flex items-center hover:text-sky-500"
                    @click="profileClick()"
                >
                    <IconUser
                        class="text-white w-[40px] h-[40px] transition-all hover:text-sky-500"
                    ></IconUser>
                    <div class="grid">
                        <label class="text-white text-[13px]">{{
                            phone
                        }}</label>
                        <label class="text-white text-[13px]">{{ name }}</label>
                    </div>
                </div>
            </div>
        </div>
        <div class="flex flex-wrap justify-center bg-white">
            <NuxtLink
                :to="'/'"
                class="p-[5px] m-[5px] hover:text-sky-500 transition-all hover:bg-slate-100 rounded-md"
            >
                Baş sahypa
            </NuxtLink>

            <NuxtLink
                :to="'/stores'"
                class="p-[5px] m-[5px] hover:text-sky-500 transition-all hover:bg-slate-100 rounded-md"
            >
                Dükanlar
            </NuxtLink>

            <NuxtLink
                :to="'/products'"
                class="p-[5px] m-[5px] hover:text-sky-500 transition-all hover:bg-slate-100 rounded-md"
            >
                Harytlar
            </NuxtLink>

            <NuxtLink
                :to="'/cars'"
                class="p-[5px] m-[5px] hover:text-sky-500 transition-all hover:bg-slate-100 rounded-md"
            >
                Awtoulaglar
            </NuxtLink>
        </div>
    </div>
</template>

<script>
import IconUser from '../components/icons/IconUser'
export default {
    name: 'HomeHeader',
    components: { IconUser },

    data() {
        return {
            phone: this.$cookies.get('phone'),
            name: this.$cookies.get('name'),
            login: true,
        }
    },

    methods: {
        profileClick() {
            if (this.$cookies.get('phone') !== undefined) {
                window.location.href = '/profile/'
            } else {
                window.location.href = '/login'
            }
        },
    },
}
</script>

<style>
.header {
    height: 90px;
    overflow: hidden;
    background: rgb(10, 35, 98);
}

.header .text label {
    font-weight: bold;
    vertical-align: middle;
    font-size: 30px;
    color: white;
}

.header .text {
    padding: 5px;
    align-items: center;
}

@media screen and (max-width: 610px) {
    .header .text label {
        font-size: 20px;
    }
}
</style>
