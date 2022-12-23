<script>



    export default {
        data(){
            return{
                indice: 0,
                intervallo: null,
                slides: [
                    {
                        image: '../assets/01.webp',
                        title: 'Marvel\'s Spiderman Miles Morale',
                        text: 'Experience the rise of Miles Morales as the new hero masters incredible, explosive new powers to become his own Spider-Man.',
                    }, {
                        image: '../assets/02.webp',
                        title: 'Ratchet & Clank: Rift Apart',
                        text: 'Go dimension-hopping with Ratchet and Clank as they take on an evil emperor from another reality.',
                    }, {
                        image: '../assets/03.webp',
                        title: 'Fortnite',
                        text: "Grab all of your friends and drop into Epic Games Fortnite, a massive 100 - player face - off that combines looting, crafting, shootouts and chaos.",
                    }, {
                        image: '../assets/04.webp',
                        title: 'Stray',
                        text: 'Lost, injured and alone, a stray cat must untangle an ancient mystery to escape a long-forgotten city',
                    }, {
                        image: '../assets/05.webp',
                        title: "Marvel's Avengers",
                        text: 'Marvel\'s Avengers is an epic, third-person, action-adventure game that combines an original, cinematic story with single-player and co-operative gameplay.',
                    }
                ]
            }
        },
        methods: {
            getImagePath(imgPath){
                return new URL(imgPath, import.meta.url).href;
            },
            previusSlides(){
                this.indice--;
                if(this.indice == -1){
                    this.indice = this.slides.length - 1;
                }
            },
            nextSlides(){
                this.indice++;
                if(this.indice == this.slides.length){
                    this.indice = 0;
                }
            },
            getSlideClick(indiceCorrente){
                this.indice = indiceCorrente;
            },
            stopCarosello(){
                clearInterval(this.intervallo);
            },
            inzioCarosello(){
                this.intervallo = setInterval(this.nextSlides, 3*1000);
            }
        },
        created(){
            this.intervallo = setInterval(this.nextSlides, 3*1000);
        }
    }



</script>

<template>



    <div class="container">
        <div class="slider-wrapper" tabindex="0">

            <div class="item">
                <img :src="getImagePath(slides[indice].image)" :alt="slides[indice].title" />
                <!-- <img :src="slides[indice].image" :alt="slides[indice].title" /> -->
                <div class="text">
                    <h3>{{ slides[indice].title }}</h3>
                    <p>
                        {{ slides[indice].text }}
                    </p>
                </div>
            </div>
           
            <div class="thumbs"  @mouseover="stopCarosello()" @mouseleave="inzioCarosello()">
                <div class="prev" @click="previusSlides()"></div>
                <div class="next" @click="nextSlides()"></div>

                <div v-for="(slide, index) in slides" :class="(index == indice) ? `active` : ``" class="thumb">
                    <!-- <img :src="slide.image" :alt="slide.title" @click="getSlideClick(index)" /> -->
                    <img :src="getImagePath(slide.image)" :alt="slide.title" @click="getSlideClick(index)" />
                </div>
            </div>

        </div>
    </div>


</template>

<style scoped>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }

    .container {
        height: 70vh;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .item {
        float: left;
        width: 700px;
        height: 300px;
        position: relative;
    }

    .item img {
        width: 100%;
        height: 100%;
        object-fit: cover;
    }

    .item .text {
        position: absolute;
        right: 20px;
        bottom: 20px;
        text-align: right;
        color: white;
    }

    .thumbs {
        float: left;
        height: 300px;
        background: #000;
        position: relative;
    }

    .thumb {
        height: calc((300px) / 5);
        opacity: 0.5;
    }

    .thumb img {
        width: 100%;
        height: 100%;
        object-fit: cover;
    }

    .thumb.active {
        border: 2px solid #ccc;
        opacity: 1;
    }

    .prev,
    .next {
        width: 20px;
        height: 20px;
        margin: 10px 0;
        border-radius: 50%;
        background: #ccc;
        position: absolute;
        left: 50%;
        transform: translate(-50%);
        cursor: pointer;
        z-index: 999;
    }

    .next {
        bottom: 0;
    }


    .prev::after {
        content: '';
        width: 10px;
        height: 10px;
        border-top: 1px solid black;
        border-right: 1px solid black;
        display: block;
        position: absolute;
        top: 35%;
        left: 50%;
        transform: translate(-50%) rotate(-45deg);
    }

    .next::before {
        content: '';
        width: 10px;
        height: 10px;
        border-top: 1px solid black;
        border-right: 1px solid black;
        display: block;
        position: absolute;
        bottom: 35%;
        left: 50%;
        transform: translate(-50%) rotate(135deg);
    }
</style>
