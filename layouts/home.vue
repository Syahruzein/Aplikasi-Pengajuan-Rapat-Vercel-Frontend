<template>
    <div>
        <!-- <NavBar /> -->
        <TopView />
        <MiddleView />
        <FooterView />
    </div>
</template>

<style >
    @import '~/assets/css/app.css';
</style>

<script scope>
import FooterView from './home/FooterView.vue'
import MiddleView from './home/MiddleView.vue'
// import NavBar from './home/NavBar.vue'
import TopView from './home/TopView.vue'

// import aos from '~/plugins/aos'
// import AOS from 'aos'
import 'aos/dist/aos.css'

export default {
    name: 'home',
    // mixins:[aos],
    components: {
        NavBar,
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
    // created ( ) {
    //     AOS.init()
    //     AOS.refresh()
    // },
    async mounted() {
    const AOS = await import('aos');
    AOS.init();
    }
    // created() { setTimeout(function () { document.querySelectorAll('.aos-animate').forEach(item => { item.classList.remove("aos-animate"); setTimeout( function (){ window.scrollTo(0, 2); },600) }) },50,this) }, beforeRouteLeave (to, from, next) { next(); window.scrollTo(0, 0); document.querySelectorAll('.aos-animate').forEach(item => { item.classList.remove("aos-animate"); }) }, beforeRouteEnter (to, from, next) { next(); window.scrollTo(0, 0); } 
}
</script>
