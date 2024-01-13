<template>
    <div class="about">
        <span style="white-space: pre-line">{{ description }}</span>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'HomeView',

    async asyncData({ params }) {
        const id = params.id
        try {
            const resp = await axios.get(
                process.env.server_ip + '/mob/stores/' + id,
            )
            return {
                description: resp.data.body_tm,
                storeName: resp.data.name,
            }
        } catch (err) {}
    },

    data() {
        return {
            description: '',
            id: '',
            items: [],
            contacts: [],
            server: process.env.server_ip,
            storeName: '',
        }
    },

    head() {
        return {
            title: this.storeName + ' - Dükan barada',
        }
    },
}
</script>
