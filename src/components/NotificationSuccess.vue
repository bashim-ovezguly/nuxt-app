<template>
    <div
        ref="notif"
        class="duration-1000 fixed flex justify-center p-[10px] text-[15px] min-w-[300px] min-h-[100px] rounded-md shadowed bg-slate-200 p-[10px] m-[10px] right-[-50%] bottom-[10px]"
        @click="hide()"
    >
        <label class="text-sky-700">{{ message }} </label>
    </div>
</template>

<script>
export default {
    props: ['message'],
    data() {
        return {}
    },

    mounted() {
        setTimeout(() => {
            this.open()
        }, 1000)
    },

    methods: {
        hide() {
            const newClass = this.$refs.notif.classList.value.replace(
                'right-[20px]',
                'right-[-50%]',
            )
            this.$refs.notif.classList.value = newClass
        },

        open() {
            this.$refs.notif.classList.add('right-[20px]')
            setTimeout(() => {
                this.hide()
            }, 3000)
        },
    },
}
</script>
