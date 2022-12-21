<template>
<div>
  <nav
    class="navbar fixed-top navbar-expand-lg pt-2 pb-2"
    data-aos="fade-down"
    data-aos-duration="1000"
    :class="{ onScroll: !view.topOfPage }"
        >
        <div class="container-fluid">
            <a class="navbar-brand" href="#" :class="{ 'onScroll': !view.topOfPage}"                        >
                <span class="logo">
                    <img src="~/assets/img/logo/apr.svg" 
                        class="rounded" alt="..."
                        >
                </span>
            </a>                 
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"><i class="fas fa-bars fas-color" :class="{ 'onScroll': !view.topOfPage}"></i></span>
            </button>
            <div class="collapse navbar-collapse justify-content-center" id="navbarSupportedContent">
                <ul class="navbar-nav">
                    <div class="col-md-4">         
                    <li class="nav-item"><a class="nav-link fs-5" :class="{ 'onScroll': !view.topOfPage}" href="#myCarousel">Beranda</a></li>                
                    </div>
                    <div class="col-md-6">
                    <li class="nav-item"><a class="nav-link fs-5" :class="{ 'onScroll': !view.topOfPage}" href="#body">Alur Pengajuan</a></li>
                    </div>
                    <div class="col-md-6">
                    <li class="nav-item"><a class="nav-link fs-5" :class="{ 'onScroll': !view.topOfPage}" href="#FooterView">Tentang Kami</a></li>
                    </div>
                </ul>
            </div>    
        </div>                    
    </nav>
    <Nuxt/>
</div>
</template>

<script>
export default {
    name: 'NavBar',
    data () {
        return {
            view: {
                topOfPage: true
            }
        }
    },
    beforeMount() {
        window.addEventListener('scroll', this.handleScroll)
    },
    methods: {
        handleScroll(){
            if(window.pageYOffset>0){
                if(this.view.topOfPage) this.view.topOfPage = false
            } else {
                if(!this.view.topOfPage) this.view.topOfPage = true
            }
        }
    },
}
</script>

<style scoped src="@/assets/css/app.css">
    
</style>