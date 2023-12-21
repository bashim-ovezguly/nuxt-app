<template>
  <div class="about">
    <span style="white-space: pre-line">{{ description }}</span>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'HomeView',
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
  async fetch() {
    this.id = this.$route.path.split('/')[2]
    await axios.get(this.server + '/mob/stores/' + this.id).then((resp) => {
      this.description = resp.data.body_tm
      this.storeName = resp.data.name
    })
  },

  head() {
    return {
      title: this.storeName + ' - Dükan barada',
    }
  },
}
</script>
