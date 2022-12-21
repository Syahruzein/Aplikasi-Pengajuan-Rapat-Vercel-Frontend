<template>
    <div id="Topview">
        <v-app id="inspire">
        <v-carousel
            cycle
            height="100vh"
            hide-delimiter-background
            show-arrows-on-hover
            delimiter-icon="mdi-minus mdi-36px"
        >
            <v-carousel-item
            class="one "
            >
                <v-overlay
                :absolute="absolute"
                :opacity="opacity"
                color="rgba(0, 0, 0, 1)"
                >
                    <v-container grid-list-xs>
                        <v-row no-gutters>
                            <v-col
                            class="pt-16 mt-16"
                            cols="12"
                            lg="12"
                            >

                                <!-- <img src="~/assets/img/logo/PENS.png" alt="pens.png"/> -->
                            </v-col>
                            <v-col
                            cols="12"
                            sm="12"
                            >
                                <h1 class="text-white">Ajukan rapat.</h1>
                                <p class="text-shadow">
                                Anda bisa mengagendakan rapat secara digital dengan
                                APR.
                            </p>
                            </v-col>
                            <v-col
                            cols="12"
                            sm="12"
                            >
                                <v-btn
                                x-large
                                color="bg-gradient-info"
                                dark
                                @click="login"
                                    >
                                    Masuk</v-btn
                                >
                            </v-col>
                        </v-row>
                    </v-container>
                </v-overlay>
            </v-carousel-item>

            <v-carousel-item
            class="second"
            >
                <v-overlay
                :absolute="absolute"
                :opacity="opacity"           
                color="rgba(0, 0, 0, 1)"
                >
                    <v-container grid-list-xs>
                        <v-row no-gutters>
                            <v-col
                            class="pt-16 mt-16"
                            cols="12"
                            lg="12"
                            align="center"
                            >

                                <!-- <img src="~/assets/img/logo/PENS.png" alt="pens.png"/> -->
                            </v-col>
                            <v-col
                            cols="12"
                            sm="12"                            
                            align="center"
                            >
                                <h1 class="text-white">Jadwal Rapat.</h1>
                                <p class="text-shadow">
                                    Jadwal rapat yang tepat, meningkatkan kualitas yang baik.
                            </p>
                            </v-col>
                            <v-col
                            cols="12"
                            sm="12"                            
                            align="center"
                            >
                                <v-btn
                                x-large
                                color="bg-gradient-info"
                                dark
                                @click="login"
                                    >
                                    Masuk</v-btn
                                >
                            </v-col>
                        </v-row>
                    </v-container>
                </v-overlay>
            </v-carousel-item>

            <v-carousel-item
            class="third"
            >
                <v-overlay
                :absolute="absolute"
                :opacity="opacity"
                color="rgba(0, 0, 0, 1)"
                >
                    <v-container grid-list-xs>
                        <v-row no-gutters>
                            <v-col
                            class="pt-16 mt-16"
                            cols="12"
                            lg="12"
                            align="end"                            
                            >

                                <!-- <img src="~/assets/img/logo/PENS.png" alt="pens.png"/> -->
                            </v-col>
                            <v-col
                            cols="12"
                            sm="12"                            
                            align="end"
                            >
                                <h1 class="text-white">Notulen rapat.</h1>
                                <p class="text-shadow">
                                    Catatan singkat mengenai jalannya rapat dengan APR.
                            </p>
                            </v-col>
                            <v-col
                            cols="12"
                            sm="12"
                            align="end"
                            >
                                <v-btn
                                x-large
                                color="bg-gradient-info"
                                dark
                                @click="login"
                                    >
                                    Masuk</v-btn
                                >
                            </v-col>
                        </v-row>
                    </v-container>
                </v-overlay>
            </v-carousel-item>
                
        </v-carousel>
    </v-app>
    </div>
</template>
<script>
export default {
    data () {
      return {
        absolute: true,
        opacity: 0.6,
      }
    },
    methods: {
        login(){
        this.$router.push('/auth/login');
        }
    }
}
</script>
<style>
    .one{
        background: url('@/assets/img/curved-images/curved12.png');
        background-size: cover;
        background-repeat: no-repeat;
    }
    .second{
        background: url('@/assets/img/curved-images/curved11.png');
        background-size: cover;
        background-repeat: no-repeat;
    }
    .third{
        background: url('@/assets/img/curved-images/curved15.jpg');
        background-size: cover;
        background-repeat: no-repeat;
    }
</style>