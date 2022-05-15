<template>
<main>
    <div id="search">
        <input @keydown.enter="search(searchText)" v-model="searchText" placeholder="cerca"> 
        <button @click="search(searchText)">vai</button>
    </div>
    <div v-if="showRes" id="resoultsSearch">
        <h1>Films</h1>
        <swiper :slides-per-view="4" :loop="true" @swiper="onSwiper" @slideChange="onSlideChange">
            <swiper-slide v-for="film in movies" :key="film.id" @mouseover="hover = true" @mouseleave="hover = false">
                <div class="card">
                    <div class="posterCard">
                        <img :src= "'https://image.tmdb.org/t/p/w342/'+  film.poster_path">
                    </div>
                    <div class="infoCard">
                        <h1>{{film.original_title}}</h1>
                        <h2>{{film.overview}}</h2>
                        <div>
                            <ul>
                                <li v-for="n in Math.round(film.vote_average / 2)" :key="n">
                                <font-awesome-icon icon="fa-solid fa-star" />
                                </li>
                                <li v-for="n in (5 - Math.round(film.vote_average / 2))" :key="n">
                                <font-awesome-icon icon="fa-regular fa-star" />
                                </li>
                            </ul>
                        </div>
                    </div>
                </div>
            </swiper-slide>
        </swiper>

        <h1>Serie TV</h1>
        <swiper :slides-per-view="4" :loop="true" @swiper="onSwiper" @slideChange="onSlideChange">
            <swiper-slide v-for="tv in series" :key="tv">
                <div class="card">
                    <img :src= "'https://image.tmdb.org/t/p/w342/'+  tv.poster_path">
                </div>
            </swiper-slide>
        </swiper>
    </div>
</main>
</template>


<script>
import axios from 'axios';

import { Navigation, Pagination } from 'swiper'
import { SwiperCore, Swiper, SwiperSlide } from 'swiper-vue2'
import 'swiper/swiper-bundle.css'

SwiperCore.use([Navigation, Pagination])

export default{
    components: {
        Swiper,
        SwiperSlide
    },

    name: 'AppMain',
    data(){
        return{
            movies: [],
            series: [],
            apiKey: '9c08889b4156aa846587f4aff22355b6',
            apiPath: 'https://api.themoviedb.org/3/search/',
            searchText: '',
        }
    },
    computed: {
        showRes () {
            return this.movies.length && this.series.length
        }
    },
    methods:{
        onSwiper (swiper) {
            console.log(swiper)
        },
        onSlideChange () {
            console.log('slide change')
        },
        search(text){
            const queryData = {
                params:{
                    api_key: this.apiKey,
                    query: text
                }
            }
            this.getMovies(queryData);
            this.getSeries(queryData);
            console.log(this.film.poster_path)
        },
        getMovies(queryData){
            this.movies = [];
            axios.get(this.apiPath+'movie', queryData).then((ris)=>{
                this.movies = ris.data.results;
            }).catch((err)=>{
                console.log(err);
            })
        },
        getSeries(queryData){
            this.series = [];
            axios.get(this.apiPath+'tv', queryData).then((ris)=>{
                this.series = ris.data.results;
            }).catch((err)=>{
                console.log(err);
            })
        }
    }
}
</script>

<style scoped lang="scss">
.img-fluid {
  max-width: 100%;
  height: auto;
}
.w-100 {
  width: 100%;
}
.ml-auto, .mx-auto {
  margin-left: auto;
}
.mr-auto, .mx-auto {
  margin-right: auto;
}

.swiper-slide{
  width: 350px;
  margin: 20px;
}

main{
    margin: 20px 50px;
 
    #search{
        display: flex;
        height: 40px;
        
        input{
            width: calc(100% - 70px);
            height: 100%;
            font-size: 30px;
            padding-left: 20px;
        }
        button{
            font-size: 30px;
            width: 70px;
            height: 100%;
        }
    }
    #resoultsSearch{
        >h1{
            margin-top: 50px;
        }
        .card:hover > .infoCard{
            display: flex;
            flex-direction: column;
        }
        .card:hover > .posterCard{
            display: none;
        }
            .card{
                cursor: pointer;
                width: 350px;
                height: 500px;
                background-repeat: no-repeat;
                background-size: cover;
                :active{
                    cursor: grabbing;
                }
                .infoCard{
                    display: none;
                    overflow: hidden;
                    text-align: center;
                    background-color: rgb(43, 43, 43);
                    height: 100%;

                    h1{
                        margin-bottom: 20px;
                    }
                    h2{
                        color: rgb(180, 180, 180);
                        font-size: 1.3rem;
                    }
                }

            }
    }
}
</style>
