<template>
  <div>
    <TopView />
        <MiddleView />
        <FooterView />
  </div>
</template>

<style >
    @import '~/assets/css/app.css';
</style>

<script>
import FooterView from '~/layouts/home/FooterView.vue'
import MiddleView from '~/layouts/home/MiddleView.vue'
// import NavBar from './home/NavBar.vue'
import TopView from '~/layouts/home/TopView.vue'

export default {
  layout: "home/NavBar",
  name: 'IndexPage',
  components: {
        // NavBar,
        TopView,
        MiddleView,
        FooterView,
        // Home,
    },
    head () {
        return {
        title: 'APR',
        meta: [
            { charset: 'utf-8' },
            { name: 'viewport', content: 'width=device-width, initial-scale=1' },
            { hid: 'description', name: 'description', content: '' },
            { name: 'format-detection', content: 'telephone=no' }
        ],
        link: [
            { href: 'https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css', rel: 'stylesheet', integrity:"sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC", crossorigin:"anonymous" }
        ],
        script: [
            { src: "https://cdn.jsdelivr.net/npm/bootstrap@5.2.0/dist/js/bootstrap.bundle.min.js", integrity:"sha384-A3rJD856KowSb7dwlZdYEkO39Gagi7vIsF0jrRAoQmDKKtQBHUuLZ9AsSv4jD4Xa", crossorigin:"anonymous"},
        ]

        }
    },
  computed: {
    currentUser() {
      return this.$store.state.authentication.user;
    }
  },
  async mounted () {
    if (!this.currentUser) {
      this.$router.push('/')
    }
    const AOS = await import('aos');
    AOS.init();
  },
}
</script>
